You can now provision cbur sidecar to use one of the following storage volumes
	- emptydir
	- Ephemeral Volume (if K8's version is > 1.xx) 
	- Persistent Volume

To enable cbur-sidecar to use a PVC you can enable the following YAML section. It also provides control over size, accessMode etc. 

```
server:
	cbur:
		persistentVolume:
			enabled: true
```


For Deployment: 
The size of the PVC can be changed and will be reflected during rolling upgrades. This will have some downtime.


For Statefulset:
