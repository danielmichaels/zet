# How to check Go module versions

When creating `zet-cmd` and using `go install` to pull the latest version,
I was having some issues where it would not grab the most recent version.

Here are some methods to find and then retrieve the version you want.

To check all existing versions:

`go list -m -version github.com/danielmichaels/zet-cmd`

A list of compatible operators when using `go install` or `go get`:

- Specific version: `@v.1.3.4`
- Specific commit: `@abcdefgh`
- Specific branch: `@main`
- Version prefix: `@v2`
- Comparison: `@>=2.1.4`
- Latest: `@latest` (most common)

Tags:

    #golang #modules


