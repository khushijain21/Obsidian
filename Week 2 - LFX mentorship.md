
What was achieved:
- Created a draft PR for zap logger - it implements array and object encoder to map zap values to Otel's - https://github.com/open-telemetry/opentelemetry-go-contrib/pull/5279
- Connected with Kayla - was provided with resources to get started on ruby

Blocker:
- Was not able to map all supported types in zap to Otel's - we may loose same data
- Was not able to get correct data type from interfaces implemented in zap

To Do:
- Dive deeper into ruby language and get started on ruby's lograge/semantic logger bridge
  
Learning Resources:
- Some of the design patterns I learnt
	- https://refactoring.guru/design-patterns/adapter - adpaters in go
	- https://refactoring.guru/design-patterns/bridge - Bridges in go
- https://betterstack.com/community/guides/scaling-go/json-in-go/ - marshalling and unmarshalling data in go
- https://betterstack.com/community/guides/logging/go/zap/#examining-zap-s-logging-api - Zap's design patterns 
- https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/logs/sdk.md - sdk implementation of logs 