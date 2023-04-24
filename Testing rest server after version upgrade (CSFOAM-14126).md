
1.  Get file list
```shell
curl -k "http://khu-cpro-restserver.khushi.svc.cluster.local:8888/cpro/v2/alertfiles?namespace=khushi&configmapName=khu-helmtestdata-restapi-configmap"
```
	
	Ouput
```shell
["/etc/config/rules","/etc/config/alerts"]
```

2. Delete file list
```shell
 curl -v -H "Content-Type: application/json" -X DELETE "http://khu-cpro-restserver.khushi.svc.cluster.local:8888/cpro/v2/alertfiles/%2Fetc%2Fconfig%2Frules?namespace=khushi&configmapName=khu-helmtestdata-restapi-configmap"
 ```

``` shell
curl -k "http://khu-cpro-restserver.khushi.svc.cluster.local:8888/cpro/v2/alertfiles?namespace=khushi&configmapName=khu-helmtestdata-restapi-configmap"
```

	output
```shell
["/etc/config/alerts"] # The file is now deleted
```

3. Add Alert File
```shell
curl -v -X POST "http://khu-cpro-restserver.khushi.svc.cluster.local:8888/cpro/v2/alertfiles?namespace=khushi&configmapName=khu-helmtestdata-restapi-configmap&fileName=/etc/config/testfiles" -H "Content-Type: application/json"
```

	output
```shell
["/etc/config/alerts","/etc/config/testfiles"]
```

4. List Alert Rules
```shell
curl -v -X GET "http://khu-cpro-restserver.khushi.svc.cluster.local:8888/cpro/v2/alertrules?namespace=khushi&configmapName=khu-helmtestdata-restapi-configmap&fileName=/etc/config/alerts" -H "Content-Type: application/json"
```
	output
``` shell
groups:

- name: "pre-defined-alert-rules"

rules:

- alert: "NodeFilesystemUsageMinor"

expr: "((node_filesystem_size_bytes{mountpoint=\"/\",device!=\"rootfs\"} - node_filesystem_avail_bytes{mountpoint=\"\

/\",device!=\"rootfs\"}) / node_filesystem_size_bytes{mountpoint=\"/\",device!=\"\

rootfs\"} * 100 > 70) and ((node_filesystem_size_bytes{mountpoint=\"/\",device!=\"\

rootfs\"} - node_filesystem_avail_bytes{mountpoint=\"/\",device!=\"rootfs\"\

}) / node_filesystem_size_bytes{mountpoint=\"/\",device!=\"rootfs\"} * 100 <=\

\ 80)"

labels:

severity: "MINOR"

name: "FileSystemExceedThreshold"

text: "Usage of file system is greater than the threshold value"

id: "3001200"

source: "CPRO"

host: "hostname"

eventType: "11"

probableCause: "351"

key: "MOC001"

annotations:

summary: "High Filesystem usage detected"

description: "Filesystem usage is above 70%"

for: "1m"
```

4. Delete Alert Rule

```shell
curl -v -X DELETE "http://roh-cpro-restserver.rohith.svc.cluster.local:8888/cpro/v2/alertrules/NodeFilesystemUsageMinor?namespace=rohith&configmapName=roh-helmtestdata-restapi-configmap&fileName=/etc/config/alerts&groupName=pre-defined-alert-rules" -H "Content-Type: application/json"
```

	output
```
< HTTP/1.1 200 OK

< Date: Fri, 10 Mar 2023 06:33:45 GMT

< Content-Length: 0

< Server: Jetty(9.4.49.v20220914)
```


5. Add Alert Rule
```
curl -v -X POST "http://roh-cpro-restserver.rohith.svc.cluster.local:8888/cpro/v2/alertrules?namespace=rohith&configmapName=roh-helmtestdata-restapi-configmap&fileName=/etc/config/alerts&groupName=pre-defined-alert-rules" -H 'accept: application/json' -H 'Content-Type: application/json' -d@alertRule.json
```

	output
```
< HTTP/1.1 200 OK
< Date: Fri, 10 Mar 2023 06:40:28 GMT

< Content-Type: application/json

< Content-Length: 1735

< Server: Jetty(9.4.49.v20220914)

```