
- Working with packages in GO [A beginners guide to Packages in Golang | CalliCoder](https://www.callicoder.com/golang-packages/)
-  Learn go with tests [quii/learn-go-with-tests: Learn Go with test-driven development (github.com)](https://github.com/quii/learn-go-with-tests)

### Benchmarking

Writing [benchmarks](https://golang.org/pkg/testing/#hdr-Benchmarks) in Go is another first-class feature of the language and it is very similar to writing tests.

```go
func BenchmarkRepeat(b *testing.B) {
	for i := 0; i < b.N; i++ {
		Repeat("a")
	}
}
```


```go
go test ./...
```

