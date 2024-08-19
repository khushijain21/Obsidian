
grafana-otel-lgtm
![[Pasted image 20240405113001.png]]

2!aFwZTFG



prereq: server.cbur must be enabled

test scenarios: 
- (for deployment)
	- cbur-storage-volume pvc must exist and include server.size
	- when server.cbur.enabled without size override, cbur-storage-volume pvc must exist and include server.size
	- when server.cbur.enabled wih existing claimname, cbur-storage-volume pvc must not exist and include server.size