
https://github.com/open-telemetry/community/issues/1982  - 1st week


Resources
https://opentelemetry.io/docs/concepts/instrumentation/code-based/ - code based implementation using OTEL api and SDK


https://github.com/open-telemetry/opentelemetry-go-contrib/issues/5138 - slog log bridge

Prototype implementation of slog handler https://github.com/pellared/opentelemetry-go/blob/147762ffb5c4394417b3f973274cc570723db79b/log/internal/slog.go

https://github.com/open-telemetry/community/issues/1865#issuecomment-1913132738  - list of bridge API's implemented

IMP** - https://github.com/open-telemetry/opentelemetry-go/blob/main/log/DESIGN.md#add-xyz-method-to-logger  - logs bridge API deign document

https://opentelemetry.io/docs/specs/otel/logs/ - log specification
Log Appenders will use Log Bridge API to export log in OTEL format

https://github.com/open-telemetry/opentelemetry-specification/issues/3917 - add an enabled method to the logger

https://github.com/golang/example/blob/master/slog-handler-guide/README.md  - guide to writing slog handler


![[appender.png]]








In addition, the requests outgoing from the application may be injected with the same trace context data, thus resulting in context propagation through the application and creating an opportunity to have full trace context in logs collected from all applications that can be instrumented in this manner.
