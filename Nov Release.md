

Sprint wise work allocation list is below. Sprint 3 is kept blank for now. 

We will use if for DoD activities and study if the remaining work finishes on time. 


CSFOAM-17905


For strict case


| Workload Name      | Container Name          | Supported Image Flavors                         | can be configure under        |
| ------------------ | ----------------------- | ----------------------------------------------- | ----------------------------- |
| Alert Manager      | InitContainer           | rocky8-python3.8)                               | initConfigFile                |
|                    | alertmanager            | (distroless)                                    | alertmanager (workload level) |
|                    | cmreload                | (distroless)                                    | configmapReload               |
|                    | util                    | rocky8-python3.8)                               | cproUtil                      |
|                    | fluentd                 | rocky8-jre17                                    | fluentd                       |
|                    | file-validator          | distroless                                      | certManagerConfig             |
| Server             | InitContainer           | rocky8-python3.8)                               | initConfigFile                |
|                    | cmreload                | (distroless)                                    | configmapReload               |
|                    | cbura-sidecar           | ?                                               | no                            |
|                    | server                  | (distroless)                                    | server (workload)             |
|                    | migrate/pre-upgrade-job | rocky8-python3.8                                | helmtest                      |
|                    | check-startup           | rocky8-python3.8                                | helmtest                      |
|                    | util                    | rocky8-python3.8)                               | cproUtil                      |
|                    | monitoringContainer     |  rocky8-python3.8                                               | monitoringContainer                              |
|                    | fluentd                 | rocky8-jre17                                    | fluentd                       |
| RestServer         | InitContainer           | rocky8-python3.8)                               | initConfigFile                |
|                    | cmreload                | (distroless)                                    | configmapReload               |
|                    | restserver              | distroless-jre17)                               | restserver                    |
|                    | restapi-test            | (rocky8-python3.8                               | helmtest                      |
|                    | fluentd                 | rocky8-jre17                                    | fluentd       \               |
|                    | file-validator          | distroless                                      | certManagerConfig             |
| Hooks              | br-hook-postrestore     |                                                 |                               |
|                    | br-hook-prebackup       | All use rocky8-nano image    (Kubectl registry) | helmDeleteImage               |
|                    | post-delete             |                                                 |                               |
|                    | pre-upgrade             |                                                 |                               |
|                    | post-upgrade            |                                                 |                               |
| Kube State Metrics | kube-state-metrics      | distroless                                      | kubeStateMetrics              |
|                    | file-validator          | distroless                                      | certManagerConfig             |
| node-exporter      | node-exporter           | distroless                                      | node-exporter                 |
|                    | file-validator          | distroless                                      | certManagerConfig             |
| webhook4fluentd    | webhook4fluentd         | distroless                                      | webhook4fluentd               |
| pushgateway        | pushgateway             | distroless                                      | pushgateway                   |
|                    |                         |                                                 |                               |


Scenarios to Test in CPRO

-   - Best match with Default imageFlavor 
-   - Expected: Template pass and renders correct images

  - Strict match at global, root or workload level with any flavor
-   - Expected: Template fails

-   - Strict match with distroless at  alertmanager, server level and configure correct supported flavors at container level
-   - Expected: Template pass and renders correct image

-   - Strict match with distroless-jre11/jre17 at  restserver level and configure correct supported flavors at container level
-   - Expected: Template pass and renders correct image


![[Pasted image 20231020181333.png]]









	



|                       | Container Name                      | Image Flavor     | can be configured under   |
| --------------------- | ----------------------------------- | ---------------- | ------------------------- |
| Grafana               | plugins sidecar (Init Container)    | (rocky8)         | pluginsSideCar            |
|                       | certManager  (Init Container)       | distroless       | certManager               |
|                       | cbura-sidecar                       | 1 (cbur-agent)   |                           |
|                       | grafana-mdb-tool                    | (rocky8)         | mdbToolImage              |
|                       | util                                | (rocky8)         | grafanaUtil               |
|                       | cpro-grafana                        | distroless       | grafana: (main container) |
|                       | grafanaSidecarDashboard             | rocky8-python3.8 | sidecar                   |
|                       | grafanaDatasource                   | rocky8-python3.8 | sidecar                   |
|                       | downloadDashboards (Init container) | rocky8           | downloadDashboardsImage   |
|                       | file-merge                          | distroless       | grafanaFileMerge          |
| grafana-test-status   | test-container                      | rocky8-nano      | helmDeleteImage           |
| post-delete-secret    | delete-secrets-container            | rocky8-nano      | helmDeleteImage           |
| delete-dashboard-job  | del-dash                            | (rocky8)         | hookImage                 |
| import_dashboard_job  | import-dashboard                    | (rocky8)         | hookImage                 |
| job                   | set-datasource                      | (rocky8)         | hookImage                 |
| post-delete-job       | post-delete-job                     | (rocky8)         | hookImage                 |
| update_datasource_job | delete-datasource                   | (rocky8)         | hookImage                 |
| post-upgrade-job      | post-upgrade-job                    | (rocky8 )        |                           |
|                       |                                     |                  |                           |


logrotate: CHAR
kubectl: CCBI


{{- $root := .root }}
{{- $containerlevel:= .containerlevel }}
{{- $workload := .workload }}
{{- $imageName := .imageName }}
{{- $supportedflavour := .supportedflavour }}
{{- $imagetag := split "-" ( toString $root.Values.image.distro.tag ) }}
image: "{{ template "cpro-common-lib.v1.imageRegistry" ( dict "root" $root "imageInfo" $root.Values.image.distro.repo "internalRegisty" $root.Values.intPromMetricsReg ) }}:{{ $imagetag._0 }}-{{ template "cpro-common-lib.imageFlavorMapper" (tuple $root.Values $workload $imageName $supportedflavour $containerlevel) }}-{{ $imagetag._1 }}"


Gen3GPPXML


|              | Container name  | Image Flavors Supported | Can be configured under |
| ------------ | --------------- | ----------------------- | ----------------------- |
| Gen3GPPXML   | gen3gppxml      | rocky8-python3.8        | gen3gppxml              | 
|              | sftp            | rocky8-python3.8        |                         |
|              | configmapreload | rocky8-python3.8        |                         |
|              | cbura-sidecar   |                         |                         |
| post-delete  |                 | rocky8-nano             | kubectl                 |
| check-status | test-container  | rocky8-nano             | kubectl                 |
|              | post-delete-pvc | rocky8-nano             | kubectl                 |
|              | fluentd         | rocky8-jre17            | fluentd                 |



|          | Container                | supported Flavors          | can be configured under |
| -------- | ------------------------ | -------------------------- | ----------------------- |
| vm-agent | vm-agent                 | distroless                 | vm-agent                |
| fluentd  | fluentd                  | rocky8-jre11, rocky8-jre17 | fluentd                 |
|          | cpro-vmc-test-status     | rocky8-nano                | helmTest                |
|          | cpro-vmagent-post-delete | rocky8-nano                | helmDeleteImage         |


|          | Container                 | supported FLavors | can be configured under |
| -------- | ------------------------- | ----------------- | ----------------------- |
| vm-alert | cpro-vm-alert             | distroless        | vm-alert                |
|          | cpro-vm-alert-test-status | rocky8-nano       | helmTest                | 
|          | fluentd                   | rocky8-jre17      | fluentd                 |




VM - SINGLE

|                    | Container                 | Supported Flavor | can be configured under |
| ------------------ | ------------------------- | ---------------- | ----------------------- |
| server-statefulset | cpro-restore (init-con)   | rocky8           | vmutils                 |
|                    | cpro-vms-util             | rocky8           | vmutils                 |
|                    |                           |                  |                         |
|                    | cpro-vmc-test-status      | rocky8 (nano)    | helmDeleteImage         |
|                    | cpro-vmsingle-post-delete | rocky8 (nano)    | helmDeleteImage         |
|                    | cpro-vm-single            | distroless       | server                  |
|                    | fluentd                   | rocky8-jre17     | fluentd                 |
|                    | cpro-vm-single-job        | rocky8 (nano)    | helmDeleteImage                        |


VM - CLUSTER


|     | container            | supported Flavors | can be configured under |
| --- | -------------------- | ----------------- | ----------------------- |
|     | vminsert             | distroless        | vmapp                   |
|     | vmselect             | distroless        | vmapp                   |
|     | vmutil-init , vmutil | rocky8            | vmutils                 |
|     | vmstorage            | distroless        | vmapp                   |
|     | cpro-vmc-test-status | rocky8 (nano)     | helmDeleteImage         |
|     | vmcluster            | rocky8 (nano)     | helmDeleteImage         |



Changes to make:
- global.imageFlavorPolicy should be empty. Remove BestMatch