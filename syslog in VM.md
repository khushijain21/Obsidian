

https://github.com/rsyslog/rsyslog/issues/2626

https://github.com/VictoriaMetrics/VictoriaMetrics/issues/2966


```bash
tail -f /var/log/syslog
```

```
# make gtls driver the default
$DefaultNetstreamDriver gtls

# certificate files
$DefaultNetstreamDriverCAFile /home/khushijain21/VictoriaMetrics/bin/ca-syslog-cert.pem
$DefaultNetstreamDriverCertFile /home/khushijain21/VictoriaMetrics/bin/syslog-cert.pem
$DefaultNetstreamDriverKeyFile /home/khushijain21/VictoriaMetrics/bin/syslog-key.pem

$ModLoad imtcp  # TCP listener
$InputTCPServerStreamDriverMode 1  # run driver in TLS-only mode
$InputTCPServerStreamDriverAuthMode anon
$InputTCPServerRun 6514  # start up listener at port 10514


```



```

global(   DefaultNetstreamDriver="gtls"   DefaultNetstreamDriverCAFile="/home/khushijain21/VictoriaMetrics/bin/ca-syslog-cert.pem"   DefaultNetstreamDriverCertFile="/home/khushijain21/VictoriaMetrics/bin/syslog-cert.pem"   DefaultNetstreamDriverKeyFile="/home/khushijain21/VictoriaMetrics/bin/syslog-key.pem"   )   

# provides TCP syslog reception with encryption
module(load="imtcp" StreamDriver.Name="gtls" StreamDriver.Mode="1" StreamDriver.AuthMode="anon")
input(type="imtcp" port="514" )


```



```
./victoria-metrics --loggerOutput=syslog --syslog-address=localhost:514 --syslog.tlsCAFile="ca-syslog-cert.pem" --syslog-network=tcp+tls
```