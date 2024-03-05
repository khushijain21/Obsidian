https://github.com/VictoriaMetrics/VictoriaMetrics/blob/master/docs/vmbackup.md


how to create openssl certificates
https://stackoverflow.com/questions/64814173/how-do-i-use-sans-with-openssl-instead-of-common-name/66980106#66980106



Vmbackup:  Provide client-side TLS configuration to create/delete snapshot

**Is your feature request related to a problem? Please descri**be

Currently, vmbackup connects to snapshot url via HTTP scheme only and it fails to connect to VM in https mode. 

**Describe the solution you'd like:**
Provide additional CLI flags for client side TLS configuration.

**Additional information:**
If the community feels this is a required feature I would like to contribute here. Also please do share if there are any better approaches for the same.
