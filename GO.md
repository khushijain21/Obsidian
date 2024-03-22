
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



What are contexts in go-lang: https://www.digitalocean.com/community/tutorials/how-to-run-multiple-functions-concurrently-in-go

How to run multiple functions concurrently: 
https://www.digitalocean.com/community/tutorials/how-to-run-multiple-functions-concurrently-in-go - from digital ocean 

https://last9.io/blog/how-to-instrument-golang-app-using-opentelemetry-tutorial-best-practices/ - how to implement open telemetry for go application

https://www.honeycomb.io/blog/ask-miss-o11y-making-sense-of-open-telemetry-tracerprovider - difference b/w tracer and tracerprovider

https://www.digitalocean.com/community/tutorials/understanding-defer-in-go - defer in go

https://www.digitalocean.com/community/tutorials/how-to-use-the-flag-package-in-go - how to use flag package in go

https://www.digitalocean.com/community/tutorials/how-to-use-interfaces-in-go - how to use interfaces in go

https://www.digitalocean.com/community/conceptual-articles/understanding-pointers-in-go  - pointers in go

https://medium.com/eureka-engineering/understanding-allocations-in-go-stack-heap-memory-9a2631b5035d - understanding variable allocation on stack and heap

https://betterprogramming.pub/memory-optimization-and-garbage-collector-management-in-go-71da4612a960 - garbage collector

https://golangforall.com/en/post/dependency-injection.html  - dependency injection

good example of type adapter:

![[Pasted image 20240318212736.png]]