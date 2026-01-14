# TIL: Go's fnv hash

A colleague introduced me to `hash/fnv` from the Go stdlib today. 

It's a very simple and fast hashing lib when you don't need cryptographic hashing.

Some use cases for me to remember:

- Hash map keys
- Deduplication

[demo](https://go.dev/play/p/YqlSV0GZ3fQ)

Tags:

    #til #hashing
