Related github Issue: https://github.com/open-telemetry/community/issues/1982

Resources for Reading: 
- Main documentation for Otel: [https://opentelemetry.io/docs/](https://opentelemetry.io/docs/)
- Log specifications for Otel https://opentelemetry.io/docs/specs/otel/logs/
- Logs Bridge API https://github.com/open-telemetry/opentelemetry-specification/blob/976432b74c565e8a84af3570e9b82cb95e1d844c/specification/logs/bridge-api.md 
- Implementation design of log Bridge API  (Golang) : https://github.com/open-telemetry/opentelemetry-go/blob/main/log/DESIGN.md
-  Guide to writing Slog Handler: https://github.com/golang/example/blob/master/slog-handler-guide/README.md  
- Prototype implementation of slog handler https://github.com/pellared/opentelemetry-go/blob/147762ffb5c4394417b3f973274cc570723db79b/log/internal/slog.go
- Zap documentation- https://pkg.go.dev/go.uber.org/zap
- (Zap Bridge ) https://github.com/keyval-dev/opentelemetry-zap-bridge

Completed: 
- List of Logging Bridges Implemented in various languages - [https://github.com/khushijain21/Obsidian/blob/main/List%20of%20Log%20Appenders%20Implemented.md](https://github.com/khushijain21/Obsidian/blob/main/List%20of%20Log%20Appenders%20Implemented.md)

To Do:
- Decide the order in which the logging bridge should be implemented