// Think of this as a stack data structure, the most nested namespace is popped out first,

// and appended to the previous namespace in the stack, and so on until root

https://betterstack.com/community/guides/logging/go/zap/#examining-zap-s-logging-api -  ZAP logging

https://github.com/keyval-dev/opentelemetry-zap-bridge - zap bridge implementation

check why dict takes so many allocations
```
BenchmarkZapWrite
=== RUN   BenchmarkZapWrite/Int
BenchmarkZapWrite/Int
BenchmarkZapWrite/Int-12                11757969               199.9 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/String
BenchmarkZapWrite/String
BenchmarkZapWrite/String-12              8667990               151.4 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/Time
BenchmarkZapWrite/Time
BenchmarkZapWrite/Time-12                8599201               128.9 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/Binary
BenchmarkZapWrite/Binary
BenchmarkZapWrite/Binary-12              8500701               126.6 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/ByteString
BenchmarkZapWrite/ByteString
BenchmarkZapWrite/ByteString-12          8146266               134.0 ns/op           179 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/Array
BenchmarkZapWrite/Array
BenchmarkZapWrite/Array-12               4013295               322.7 ns/op           272 B/op          6 allocs/op
=== RUN   BenchmarkZapWrite/Object
BenchmarkZapWrite/Object
BenchmarkZapWrite/Object-12              3416290               311.8 ns/op           320 B/op          5 allocs/op
=== RUN   BenchmarkZapWrite/Map
BenchmarkZapWrite/Map
BenchmarkZapWrite/Map-12                 2030032               603.5 ns/op           312 B/op          8 allocs/op
=== RUN   BenchmarkZapWrite/Dict
BenchmarkZapWrite/Dict
BenchmarkZapWrite/Dict-12                3340764               373.0 ns/op           320 B/op          5 allocs/op
=== RUN   BenchmarkZapWrite/Context
BenchmarkZapWrite/Context
BenchmarkZapWrite/Context-12             6801388               183.8 ns/op           176 B/op          3 allocs/op
PASS
ok      go.opentelemetry.io/contrib/bridges/otelzap     17.530s
```

after pooling
```
goos: linux
goarch: amd64
pkg: go.opentelemetry.io/contrib/bridges/otelzap
cpu: 12th Gen Intel(R) Core(TM) i5-1245U
=== RUN   BenchmarkZapWrite
BenchmarkZapWrite
=== RUN   BenchmarkZapWrite/Int
BenchmarkZapWrite/Int
BenchmarkZapWrite/Int-12                 6603409               184.7 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/String
BenchmarkZapWrite/String
BenchmarkZapWrite/String-12              5729554               207.4 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/Time
BenchmarkZapWrite/Time
BenchmarkZapWrite/Time-12                4884952               252.3 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/Binary
BenchmarkZapWrite/Binary
BenchmarkZapWrite/Binary-12              5407634               195.5 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/ByteString
BenchmarkZapWrite/ByteString
BenchmarkZapWrite/ByteString-12          5737693               196.5 ns/op           179 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/Array
BenchmarkZapWrite/Array
BenchmarkZapWrite/Array-12               4738774               231.6 ns/op           176 B/op          3 allocs/op
=== RUN   BenchmarkZapWrite/Object
BenchmarkZapWrite/Object
BenchmarkZapWrite/Object-12              3924092               320.4 ns/op           320 B/op          5 allocs/op
=== RUN   BenchmarkZapWrite/Map
BenchmarkZapWrite/Map
BenchmarkZapWrite/Map-12                 1919893               566.1 ns/op           312 B/op          8 allocs/op
=== RUN   BenchmarkZapWrite/Dict
BenchmarkZapWrite/Dict
BenchmarkZapWrite/Dict-12                3554661               304.6 ns/op           320 B/op          5 allocs/op
=== RUN   BenchmarkZapWrite/Context
BenchmarkZapWrite/Context
BenchmarkZapWrite/Context-12             6546847               164.1 ns/op           176 B/op          3 allocs/op
```


After pointer 
```
goos: linux
goarch: amd64
pkg: go.opentelemetry.io/contrib/bridges/otelzap
cpu: 12th Gen Intel(R) Core(TM) i5-1245U
=== RUN   BenchmarkZapWrite
BenchmarkZapWrite
=== RUN   BenchmarkZapWrite/Int
BenchmarkZapWrite/Int
BenchmarkZapWrite/Int-12                 8276072               155.3 ns/op           200 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/String
BenchmarkZapWrite/String
BenchmarkZapWrite/String-12              6223702               169.6 ns/op           200 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/Time
BenchmarkZapWrite/Time
BenchmarkZapWrite/Time-12                7738730               155.8 ns/op           200 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/Binary
BenchmarkZapWrite/Binary
BenchmarkZapWrite/Binary-12              7142481               157.8 ns/op           200 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/ByteString
BenchmarkZapWrite/ByteString
BenchmarkZapWrite/ByteString-12          7271110               185.2 ns/op           203 B/op          5 allocs/op
=== RUN   BenchmarkZapWrite/Array
BenchmarkZapWrite/Array
BenchmarkZapWrite/Array-12               7112994               182.0 ns/op           200 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/Object
BenchmarkZapWrite/Object
BenchmarkZapWrite/Object-12              5997675               219.1 ns/op           200 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/Map
BenchmarkZapWrite/Map
BenchmarkZapWrite/Map-12                 2403025               670.3 ns/op           336 B/op          9 allocs/op
=== RUN   BenchmarkZapWrite/Dict
BenchmarkZapWrite/Dict
BenchmarkZapWrite/Dict-12                4856680               256.0 ns/op           200 B/op          4 allocs/op
=== RUN   BenchmarkZapWrite/Context
BenchmarkZapWrite/Context
BenchmarkZapWrite/Context-12             5024188               230.3 ns/op           200 B/op          4 allocs/op
PASS
ok      go.opentelemetry.io/contrib/bridges/otelzap     17.128s
```


```
goos: linux
goarch: amd64
pkg: go.opentelemetry.io/contrib/bridges/otelzap
cpu: 12th Gen Intel(R) Core(TM) i5-1245U
=== RUN   BenchmarkMultipleFields
BenchmarkMultipleFields
=== RUN   BenchmarkMultipleFields/With_10_fields
BenchmarkMultipleFields/With_10_fields
BenchmarkMultipleFields/With_10_fields-12                2270601               546.1 ns/op           780 B/op          5 allocs/op
=== RUN   BenchmarkMultipleFields/With_20_fields
BenchmarkMultipleFields/With_20_fields
BenchmarkMultipleFields/With_20_fields-12                1000000              1108 ns/op            1696 B/op          6 allocs/op
PASS
ok      go.opentelemetry.io/contrib/bridges/otelzap     2.911s
```