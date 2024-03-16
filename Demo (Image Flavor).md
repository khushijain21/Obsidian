

**Image Flavor and Image Flavor Policy**

Image Flavor is now supported for all containers and can be configured in values.yaml
ImageFlavorPolicy supports BestMatch and Strict case

Image Flavor takes following Precedence

	container.imageFlavor > workload.imageFlavor > root.imageFlavor global.imageFlavor

#### Exceptions:
- Cbur and logrotate currently do not support any image flavor hence they are excepted from this
- For kubectl Image - nano is part of the tag and rocky8 is the supported Image Flavor

#### Notes:
- To not change __defaultFlavor in values.yaml
- Tag Name should now follow this convention in the chart
```
## If tag is 9.8.7-rocky8-98989
tag: 9.8.7-989898 (Flavor should not be part of the tag)
```



| Container Name                                   | Supported Image Flavors | can be configured under |
| ------------------------------------------------ | ----------------------- | ----------------------- |
| InitContainer(for all workloads)                 | rocky8-python3.8        | initConfigFile          |
| cmreload                                         | distroless              | configmapReload         |
| util                                             | rocky8-python3.8        | cproUtil                |
| fluentd                                          | rocky8-jre17            | fluentd                 |
| file-validator                                   | distroless              | certManagerConfig       |
| monitoringContainer (under server)               | rocky8-python3.8        | monitoringContainer     |
| server (main container)                          | distroless              | server                  |
| alertmanager (main container)                    | distroless              | alertmanager            |
| restserver (main container)                      | distroless-jre17        | restserver              |
| kube-state-metrics                               | distroless              | kubeStateMetrics        |
| node-exporter                                    | distroless              | nodeExporter            |
| webhook4fluentd                                  | distroless              | webhook4fluentd         |
| pushgateway                                      | distroless              | pushgateway             |
| restapi-test,       check-startup                | rocky8-python3.8        | helmtest                |
| All Hooks and migrate/ pre and post upgrade jobs | rocky8 (nano)           | helmDeleteImage         |


Scenarios Tested (CPRO)

- Template fails when incorrect Image Flavor is configured at global/root level
-  Template pass when correct Image Flavor is configured at global/root level (Best Match)
- Template fails when imageFlavor is configured at workload level (workload w/ multiple containers) but not for all containers in Strict Case

-  Default case (when no image flavor is set) - all containers are checked for correct Image tag, build and flavor 
-    ImageFlavor at global Level  is set
	- ImageFlavorPolicy at global level is set to Strict
	- All containers are set w/ supported Image Flavor 
	- Test Case Passes


![[Pasted image 20231110154536.png]]

| Container                                | Supported Flavor | can be configured under   |
| ---------------------------------------- | ---------------- | ------------------------- |
| plugins sidecar (Init Container)         | (rocky8)         | pluginsSideCar            |
| certManager (Init Container)             | distroless       | certManager               |
| grafana-mdb-tool                         | (rocky8)         | mdbToolImage              |
| util                                     | rocky8           | grafanaUtil               |
| cpro-grafana                             | distroless       | grafana: (main container) |
| grafanaSidecarDashboard                  | rocky8-python3.8 | sidecar                   |
| grafanaDatasource                        | rocky8-python3.8 | sidecar                   |
| downloadDashboards (Init container)      | rocky8           | downloadDashboardsImage   |
| file-merge                               | distroless       | grafanaFileMerge          |
| test container, delete-secrets-container | rocky8(nano)     | helmDeleteImage           |
| All jobs                                 | rocky8           | hookImage                          |


![[Pasted image 20231110155419.png]]



