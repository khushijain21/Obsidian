

How to start using OTLP logging natively with zap (Golang)

Logs are the quickest way to get insights into your application. With OTel standardization users will be able collate, correlate and visualize telemetry data easily.

For this demo - we are choosing zap library by Uber and stdout as the exporter. You can also export your logs to an OTLP endpoint and use visualization tools for trace-log correlation.


![[Pasted image 20240709100025.png]]
					Flow of log data in this code example

1. Initialize a loggerProvider

```
go get go.opentelemetry.io/otel \
  go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploghttp \
  go.opentelemetry.io/otel/sdk \
  go.opentelemetry.io/otel/sdk/log
```

```go
// from original OTel documentation
package main

import (
	"context"
	"fmt"

	"go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploghttp"
	"go.opentelemetry.io/otel/log/global"
	"go.opentelemetry.io/otel/sdk/log"
	"go.opentelemetry.io/otel/sdk/resource"
	semconv "go.opentelemetry.io/otel/semconv/v1.21.0"
)

func main() {
	ctx := context.Background()

	// Create resource.
	res, err := newResource()
	if err != nil {
		panic(err)
	}

	// Create a logger provider.
	// You can pass this instance directly when creating bridges.
	loggerProvider, err := newLoggerProvider(ctx, res)
	if err != nil {
		panic(err)
	}

	// Handle shutdown properly so nothing leaks.
	defer func() {
		if err := loggerProvider.Shutdown(ctx); err != nil {
			fmt.Println(err)
		}
	}()

	// Register as global logger provider so that it can be accessed global.LoggerProvider.
	// Most log bridges use the global logger provider as default.
	// If the global logger provider is not set then a no-op implementation
	// is used, which fails to generate data.
	global.SetLoggerProvider(loggerProvider)
}

func newResource() (*resource.Resource, error) {
	return resource.Merge(resource.Default(),
		resource.NewWithAttributes(semconv.SchemaURL,
			semconv.ServiceName("my-service"),
			semconv.ServiceVersion("0.1.0"),
		))
}

func newLoggerProvider(ctx context.Context, res *resource.Resource) (*log.LoggerProvider, error) {
	exporter, err := otlploghttp.New(ctx)
	if err != nil {
		return nil, err
	}
	processor := log.NewBatchProcessor(exporter)
	provider := log.NewLoggerProvider(
		log.WithResource(res),
		log.WithProcessor(processor),
	)
	return provider, nil
}

```

2. Import otelzap 

```
go get "go.opentelemetry.io/contrib/bridges/otelzap"
```

 Initialize the logger

``` go
// Add this logic to the main function above
func main(){

	// This will use globally set LoggerProvider
	// If not set, it uses no-op implementation and fails to generate data
	logger := zap.New(otelzap.NewCore("my/pkg/name")

    // You can now use your logger in your code.
    logger.Info("something really cool")
    
    // Add context for trace correlation
    logger.Info("Add tract context", zap.Reflect("ctx",      ctx.Background()))
}
```

This is how you can setup logging with OTel and zap. I hope you find this useful. 


traces, metrics and logs are like different lenses through which you choose to observe your application. You change this lens as you ask different questions to it. How many requests did you serve. How many of the the served request failed? Which instance of pod in the cluster is down? It is always best to first choose your question - and then select your signal. The  easiest observability solution used are logs. And metrics follow. Traces are also gaining traction since they are more granular but also storage intensive. 


OTEL Demo:


