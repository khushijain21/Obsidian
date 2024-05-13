
By default, zap uses console  encoder which converts the structured context into bytes and emits them to `io.Writer`.

- Should we read from the output of `io.Writer` and convert the values to otel format? 
- Or choose to implement our own encoder and perform the conversion there

```go
func (o *Core) Write(ent zapcore.Entry, fields []zapcore.Field) error {
    m := zapcore.NewMapObjectEncoder()

    for _, f := range fields {

        f.AddTo(m)

    }

  

    a := make([]log.KeyValue, 0)

    for k, v := range m.Fields {

        a = append(a, log.KeyValue{Key: k, Value: convertValue(v)})

    }

    fmt.Println(a)

    return nil

}

  

// Not complete

func convertValue(v interface{}) log.Value {

    switch reflect.TypeOf(v).Kind() {

    case reflect.String:

        return log.StringValue(v.(string))

    default:

        return log.StringValue("default")

    }

}
```