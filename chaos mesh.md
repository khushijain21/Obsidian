
```
kubectl port-forward -n chaos-mesh svc/chaos-dashboard 2333:2333
```

```
kubectl annotate ns $NAMESPACE chaos-mesh.org/inject=enabled
```


--set dashboard.securityMode=false

```
./victoria-metrics --loggerOutput=syslog --syslog.tlsCAFile="./ca-syslog-cert.pem" --syslog-address=localhost:514 --syslog-network="tcp+tls"
```



In Go, the `log/syslog` package provides a native interface to the syslog logging system. However, it doesn't provide advanced features like fault tolerance or error handling in case the syslog server is down.

If the syslog server (`rsyslog` in your case) is suddenly down, and your Go application is using the `log/syslog` package to send log messages, here's what typically happens:

1. **Blocking Behavior**: By default, when your Go application tries to send a log message using `log/syslog`, it will block until the message is successfully sent or until it times out. If the syslog server is down, this blocking behavior might cause your application to hang or experience delays until the syslog operation completes or times out.
    
2. **Error Handling**: If the syslog server is down or unreachable, the `syslog` package might return an error indicating the failure to send the log message. It's essential to handle these errors appropriately in your code to prevent unexpected behavior or crashes.
    
3. **Logging Backends**: Some applications might use `log/syslog` as one of several logging backends, alongside file-based logging or other mechanisms. In such cases, if the syslog server is down, the application might fall back to other logging mechanisms to ensure that log messages are still captured and recorded somewhere.
    
4. **Potential Loss of Logs**: If the syslog server is down for an extended period, log messages sent by your Go application during this time might be lost. It's essential to have a strategy in place for handling such situations, such as buffering log messages locally and retrying delivery once the syslog server becomes available again.
    

To mitigate issues related to syslog server downtime, consider implementing additional error handling and fault-tolerance mechanisms in your Go application, such as:

- Implementing retry logic for failed syslog operations.
- Using asynchronous logging mechanisms to prevent blocking behavior.
- Logging to multiple destinations simultaneously (e.g., syslog and local files) to ensure redundancy.
- Monitoring the status of the syslog server and taking appropriate action if it becomes unavailable (e.g., switching to a backup syslog server).
