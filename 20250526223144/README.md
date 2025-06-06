# Go: errors.As versus type assertions

I prefer to use error unwrapping via `errors.As` and here is my reasoning.


## Examples

Type assertion:

```go
// fails if error is wrapped
if newErr, ok := err.(*new.Error); ok {
    // only works for direct new.Error instances
}
```

Error unwrapping

```go
// works with wrapped errors like fmt.Errorf("foo: %w", newErr)
var newErr *new.Error
if errors.As(err, &newErr) {
    // finds new.Error even if wrapped
}
```

## Reasoning 

- Introduced in `1.13` alongside `errors.Is` and `fmt.Errorf("%w",err)` to fix type assertion issues.
- Type assertion is brittle (I personally try to avoid it when possible, sometimes unavoidable).
- Recommended by Go team, https://go.dev/blog/go1.13-errors
- If, in future, we decided to wrap this error, a type assertion will break; `errors.As` will still work.

## Realworld Example

I use this (sometimes) in my projects to enforce some sane error handling when processing JSON. Standard json errors can be hard to decern the true issue.

This block uses several error handling techniques where they make sense with heavy use of `errors.As` throughout. Much of this was taken from [Alex Edwards][lgf]
who provides many great resources and tools for Gophers.

```go 
func readJSON(w http.ResponseWriter, r *http.Request, dst interface{}) error {
	// Set a max body length. Without this it will accept unlimited size requests
	maxBytes := 1_048_576 // 1MB
	r.Body = http.MaxBytesReader(w, r.Body, int64(maxBytes))

	// Init a Decoder and call DisallowUnknownFields() on it before decoding.
	// This means that JSON from the client will be rejected if it contains keys
	// which do not match the target destination struct. If not implemented,
	// the decoder will silently drop unknown fields - this will raise an error instead.
	dec := json.NewDecoder(r.Body)
	dec.DisallowUnknownFields()

	// decode the request body into the target struct/destination
	err := dec.Decode(dst)
	if err != nil {
		// start triaging the various JSON related errors
		var syntaxError *json.SyntaxError
		var unmarshallTypeError *json.UnmarshalTypeError
		var invalidUnmarshallError *json.InvalidUnmarshalError

		switch {
		// Use the errors.As() function to check whether the error has the
		// *json.SyntaxError. If it does, then return a user-readable error
		// message including the location of the problem
		case errors.As(err, &syntaxError):
			return fmt.Errorf(
				"body contains badly-formed JSON (at character %d)",
				syntaxError.Offset,
			)

		// Decode() can also return an io.ErrUnexpectedEOF for JSON syntax errors. This is
		// checked for with errors.Is() and returns a generic error message to the client.
		case errors.Is(err, io.ErrUnexpectedEOF):
			return errors.New("body contains badly-formed JSON")

		// Wrong JSON types will return an error when they do not match the target destination
		// struct.
		case errors.As(err, &unmarshallTypeError):
			if unmarshallTypeError.Field != "" {
				return fmt.Errorf(
					"body contains incorrect JSON type for field %q",
					unmarshallTypeError.Field,
				)
			}
			return fmt.Errorf(
				"body contains incorrect JSON type (at character %d)",
				unmarshallTypeError.Offset,
			)

		// An EOF error will be returned by Decode() if the request body is empty. Use errors.Is()
		// to check for this and return a human-readable error message
		case errors.Is(err, io.EOF):
			return errors.New("body must not be empty")

		// If JSON contains a field which cannot be mapped to the target destination
		// then Decode will return an error message in the format "json: unknown field "<name>""
		// We check for this, extract the field name and interpolate it into an error
		// which is returned to the client
		case strings.HasPrefix(err.Error(), "json: unknown field "):
			fieldName := strings.TrimPrefix(err.Error(), "json: unknown field ")
			return fmt.Errorf("body contains unknown key %s", fieldName)

		// If the request body exceeds maxBytes the decode will fail with a
		// "http: request body too large".
		case err.Error() == "http: request body too large":
			return fmt.Errorf("body must not be larger than %d bytes", maxBytes)

		// A json.InvalidUnmarshallError will be returned if we pass a non-nil pointer
		// to Decode(). We catch and panic, rather than return an error.
		case errors.As(err, &invalidUnmarshallError):
			panic(err)

		// All else fails, return an error as-is
		default:
			return err
		}
	}

	// Call Decode() again, using a pointer to anonymous empty struct as the
	// destination. If the body only has one JSON value then an io.EOF error
	// will be returned. If there is anything else, extra data has been sent
	// and we craft a custom error message back to the client
	err = dec.Decode(&struct{}{})
	if err != io.EOF {
		return errors.New("body must only contain a single JSON value")
	}
	return nil
}
```

Tags:

    #go

[lgf]: https://lets-go-further.alexedwards.net/
