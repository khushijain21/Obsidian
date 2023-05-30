![[Pasted image 20230508145314.png]]


![[Pasted image 20230508145326.png]]




CPRO - GRAFANA
https://build8.cci.nokia.net/job/CTO/job/CSF/job/Common/job/common-tests/job/cpro-grafana_incubator/1/consoleFull



1. Custom Labels and Annotations


(Deprecated)
 >Kubernetes objects should support custom annotations per each workload defined in the `custom.<workload name>.annotations` parameter. 

Changes Required - 
	 


2.  PSP

> **`PodSecurityPolicy` object annotations should be configurable** (Recommendation)

>**Naming convention of the `values.yaml` for `PodSecurityPolicy` object annotations.**
```
rbac:
  psp:
    annotations:
      <annotations map>
```



| Chart Name                                        | Old Way                                       | New way                                       | Test Cases                                                     |
| ------------------------------------------------- | --------------------------------------------- | --------------------------------------------- | -------------------------------------------------------------- |
| Gen3GPPXML                                        | custom.gen3gppxmlSts.labels                   | gen3gppxml.labels                             | unit-tests/test_cstm_labels_and_annotations.yaml               |
|                                                   | custom.gen3gppxmlSts.annotations              | gen3gppxml.annotations                        | unit-tests/test_cstm_labels_and_annotations.yaml               |
| (Needs confirmation)                              | custom.pod.labels                             | gen3gppxml.labels                             |                                                                |
| (Needs confirmation)                              | custom.pod.annotations                        | gen3gppxml.annotations                        |                                                                |
| (Needs confirmation)                              | custom.pod.apparmorAnnotations                | gen3gppxml.annotations                        |                                                                |
|                                                   |                                               |                                               |                                                                |
| VM-Cluster                                        | custom.vmcluster.labels                       | NA                                            |                                                                |
|                                                   | custom.vmcluster.annotations                  | NA                                            |                                                                |
|                                                   | custom.vminsert.labels                        | vminsert.labels                               | unit-tests/test_workload_labels_ann.yaml                       |
|                                                   | custom.vminsert.annotations                   | vminsert.annotations                          | unit-tests/test_workload_labels_ann.yaml                       |
|                                                   | custom.vmselect.labels                        | vmselect.labels                               | unit-tests/test_workload_labels_ann.yaml                       |
|                                                   | custom.vmselect.annotations                   | vmselect.annotations                          | unit-tests/test_workload_labels_ann.yaml                       |
|                                                   | custom.vmstorage.labels                       | vmstorage.labels                              | unit-tests/test_workload_labels_ann.yaml                       |
|                                                   | custom.vmstorage.annotations                  | vmstorage.annotations                         | unit-tests/test_workload_labels_ann.yaml                       |
| (Needs confirmation)                              | custom.pod.labels                             | helmTest.labels                               |                                                                |
| (Needs confirmation)                              | custom.pod.annotations                        | helmTest.annotations                          |                                                                |
|                                                   |                                               |                                               |                                                                | 
| CPRO                                              | custom.cproSts.labels                         | server.labels                                 |                                                                |
|                                                   | custom.cproSts.annotations                    | server.annotations                            |                                                                |
|                                                   | custom.cproDeployment.labels                  | server.labels                                 |                                                                |
|                                                   | custom.cproDeployment.annotations             | server.annotations                            |                                                                |
|                                                   | custom.alertManagerSts.labels                 | alertmanager.labels                           | unit-tests/test_cstm_labels_and_annotations-alertmanager.yaml  |
|                                                   | custom.alertManagerSts.annotations            | alertmanager.annotations                      | unit-tests/test_cstm_labels_and_annotations-alertmanager.yaml  |
| AlertManager STS and deployment may also conflict | custom.alertManagerDeployment.labels          | alertmanager.labels                           | unit-tests/test_cstm_labels_and_annotations-alertmanager.yaml  |
|                                                   | custom.alertManagerDeployment.annotations     | alertmanager.annotations                      | unit-tests/test_cstm_labels_and_annotations-alertmanager.yaml  |
|                                                   | custom.kubeStateMetricsDeployment.labels      | kubeStateMetrics.labels                       | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.kubeStateMetricsDeployment.annotations | kubeStateMetrics.annotations                  | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.nodeExporterDaemonSet.labels           | nodeExporter.labels                           | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.nodeExporterDaemonSet.annotations      | nodeExporter.annotations                      | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.pushGatewayDeployment.labels           | pushgateway.labels                            | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.pushGatewayDeployment.annotations      | pushgateway.annotations                       | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.restServerDeployment.labels            | restserver.labels                             | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.restServerDeployment.annotations       | restserver.annotations                        | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.webhook4FluentdDeployment.labels       | webhook4fluentd.labels                        | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.webhook4FluentdDeployment.annotations  | webhook4fluentd.annotations                   | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.zombieExporterDaemonSet.labels         | zombieExporter.labels                         | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
|                                                   | custom.zombieExporterDaemonSet.annotations    | zombieExporter.annotations                    | unit-tests/cstm_labels_and_annotations-otherCproWorkloads.yaml |
| (Needs confirmation)                              | custom.pod.apparmorAnnotations                | global.annotations/  < workload >.annotations |                                                                |
| (Needs confirmation)                              | custom.pod.annotations                        | global.annotations/  < workload >.annotations |                                                                |
| (Needs confirmation)                              | custom.pod.labels                             | global.labels/  < workload >.labels           |                                                                |
|                                                   |                                               |                                               |                                                                |
| VM-alert                                          | custom.vmalert.labels                         | vmalert.labels                                |                                                                |
|                                                   | custom.vmalert.annotations                    | vmalert.annotations                           |                                                                |







CPRO -  [HBP v3.1.0] custom labels and annotations for kube-state-metrics, Node-exporter, Zombie-exporter, pushgateway, webhook4fluentd, restserver

![[Pasted image 20230503110630.png]]

CPRO - [HBP v3.1.0] custom labels and annotations for alertmanager

![[Pasted image 20230503110744.png]]

CPRO : [HBP v3.1.0] custom labels and annotations on cpro-server

![[Pasted image 20230503104446.png]]

Grafana - [HBP v3.1.0] custom labels and annotations

![[Pasted image 20230503105008.png]]

Gen3GPPXML - 
![[Pasted image 20230503105619.png]]

```
#  kind: ["ServiceAccount"]

          #   name: "ht-release-test-cpro-vm-cluster"

          #   expectedExistence: mustExist

          #   fields:

          #   - key: "$.metadata.annotations.'test_annot1'"

          #     expectedExistence: mustExist

          #     expectedValue: "custom_helmTest_annot_1"

          #   - key: "$.metadata.labels.'test_label1'"

          #     expectedExistence: mustExist

          #     expectedValue: "custom_helmTest_label_1"

          # - kind: ["Role"]

          #   name: "ht-release-test-cpro-vm-cluster-test-status"

          #   expectedExistence: mustExist

          #   fields:

          #   - key: "$.metadata.annotations.'test_annot1'"

          #     expectedExistence: mustExist

          #     expectedValue: "custom_helmTest_annot_1"

          # - kind: ["RoleBinding"]

          #   name: "ht-release-test-cpro-vm-cluster-test-status"

          #   expectedExistence: mustExist

          #   fields:

          #   - key: "$.metadata.annotations.'test_annot1'"

          #     expectedExistence: mustExist

          #     expectedValue: "custom_helmTest_annot_1"
```