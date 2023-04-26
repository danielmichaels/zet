# Go: simple background task

A really simple background worker snippet. Far from perfect!

```go
func background(fn func()) {
	// Launch a background goroutine.
	var wg sync.WaitGroup
	wg.Add(1)
	go func() {
		// Recover any panic.
		defer func() {
			if err := recover(); err != nil {
        // zerolog
				logger.Error().Err(fmt.Errorf("%s", err)).Msg("background-task")
			}
		}()

		// Execute the arbitrary function that we passed as the parameter.
		wg.Done()
		fn()
	}()
	wg.Wait()
}
```

Tags:

    #go #snippet
