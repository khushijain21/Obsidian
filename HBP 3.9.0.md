HBP_Kubernetes_API_

**HBP_Helm_Templates_2**  - https://docs.ext.net.nokia.com/csf/bp/helm/upcoming/HBP-All-in-one.html#hbp_helm_templates_2


https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#emptydirvolumesource-v1-core  - emptydir


If ".Capabilities.KubeVersion" is used in chart only for identifying api versions then those has to be replaced with ".Capabilities.APIVersions.Has". eg [https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-grafana/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l808](https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-grafana/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l808 "https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=csf-charts.git;a=blob;f=cpro-grafana/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l808")

No need to change in other places eg [https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-vm-cluster/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l779](https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-vm-cluster/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l779 "https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=csf-charts.git;a=blob;f=cpro-vm-cluster/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l779") where we are checking for presence of seccompProfile in securiyContext.

"Note also that CSF charts may skip checking for kubernetes version outside the CSF supported scope" is present in HBP. We can remove all code which is checking for older k8s version. "Kubernetes versions to be supported for a release can be derived from [here](https://confluence-app.ext.net.nokia.com/display/CSFDEV/Anycloud+Support "https://confluence-app.ext.net.nokia.com/display/csfdev/anycloud+support")" this is present in any cloud requirement [https://docs.ext.net.nokia.com/csf/bp/anycloud/restructure/ANYCloud-All-in-one.html#anycloud_k8s_api_1](https://docs.ext.net.nokia.com/csf/bp/anycloud/restructure/ANYCloud-All-in-one.html#anycloud_k8s_api_1 "https://docs.ext.net.nokia.com/csf/bp/anycloud/restructure/anycloud-all-in-one.html#anycloud_k8s_api_1")

https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core  