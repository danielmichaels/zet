# Golang: case statements with an OR clause

TIL how to use Go's switch and case statement with `||` (logical OR)
like functionality:

```go
switch foo {
  case "thing", "things":
    println("captured both")
  default:
    println(foo)
}
```

Reference: 

- https://go.dev/ref/spec#Switch_statements

Tags:

    #go

