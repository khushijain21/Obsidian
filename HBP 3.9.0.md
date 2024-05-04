HBP_Kubernetes_API_

**HBP_Helm_Templates_2**  - https://docs.ext.net.nokia.com/csf/bp/helm/upcoming/HBP-All-in-one.html#hbp_helm_templates_2


https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#emptydirvolumesource-v1-core  - emptydir


If ".Capabilities.KubeVersion" is used in chart only for identifying api versions then those has to be replaced with ".Capabilities.APIVersions.Has". eg [https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-grafana/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l808](https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-grafana/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l808 "https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=csf-charts.git;a=blob;f=cpro-grafana/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l808")

No need to change in other places eg [https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-vm-cluster/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l779](https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-CHARTS.git;a=blob;f=cpro-vm-cluster/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l779 "https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=csf-charts.git;a=blob;f=cpro-vm-cluster/templates/_helpers.tpl;hb=51bfaf3acb2be020cbb7e2e43795dfe3e624908e#l779") where we are checking for presence of seccompProfile in securiyContext.

"Note also that CSF charts may skip checking for kubernetes version outside the CSF supported scope" is present in HBP. We can remove all code which is checking for older k8s version. "Kubernetes versions to be supported for a release can be derived from [here](https://confluence-app.ext.net.nokia.com/display/CSFDEV/Anycloud+Support "https://confluence-app.ext.net.nokia.com/display/csfdev/anycloud+support")" this is present in any cloud requirement [https://docs.ext.net.nokia.com/csf/bp/anycloud/restructure/ANYCloud-All-in-one.html#anycloud_k8s_api_1](https://docs.ext.net.nokia.com/csf/bp/anycloud/restructure/ANYCloud-All-in-one.html#anycloud_k8s_api_1 "https://docs.ext.net.nokia.com/csf/bp/anycloud/restructure/anycloud-all-in-one.html#anycloud_k8s_api_1")

https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core  


**HBP_Kubernetes_API_1**

1. CPRO
```sh
$ grep -inr "alpha"
README.md:397:`rbac.psp.annotations` | PSP annotations that need to be added | `seccomp.security.alpha.kubernetes.io/allowedProfileNames: *,seccomp.security.alpha.kubernetes.io/defaultProfileName: runtime/default`
values.yaml:322:      seccomp.security.alpha.kubernetes.io/allowedProfileNames: runtime/default
values.yaml:323:      seccomp.security.alpha.kubernetes.io/defaultProfileName: runtime/default
values.yaml:377:      seccomp.security.alpha.kubernetes.io/allowedProfileNames: "*"
values.yaml:378:      seccomp.security.alpha.kubernetes.io/defaultProfileName: runtime/default
templates/certificate-issuer.yaml:3:{{- $useV1alpha3 := and (.Capabilities.APIVersions.Has "cert-manager.io/v1alpha3/Certificate") (not (.Capabilities.APIVersions.Has "cert-manager.io/v1/Certificate")) }}
templates/certificate-issuer.yaml:4:{{- if $useV1alpha3 }}
templates/certificate-issuer.yaml:5:apiVersion: cert-manager.io/v1alpha3
templates/webhook4fluentd/webhook4fluentd-istio-policy.yaml:3:apiVersion: "authentication.istio.io/v1alpha1"
templates/restserver/restserver-istio-policy.yaml:3:apiVersion: "authentication.istio.io/v1alpha1"
templates/server/server-istio-policy.yaml:4:apiVersion: "authentication.istio.io/v1alpha1"
templates/_apiversion.tpl:64:{{- else if .Capabilities.APIVersions.Has "cert-manager.io/v1alpha3/Certificate" }}
templates/_apiversion.tpl:65:{{- print "cert-manager.io/v1alpha3" }}
templates/_apiversion.tpl:67:{{- print "cert-manager.io/v1alpha2" }}
templates/_apiversion.tpl:81:{{- print "networking.istio.io/v1alpha3" }}
templates/_apiversion.tpl:91:{{- print "networking.istio.io/v1alpha3" }}
templates/_apiversion.tpl:101:{{- print "networking.istio.io/v1alpha3" }}
templates/pushgateway/pushgateway-istio-policy.yaml:3:apiVersion: "authentication.istio.io/v1alpha1"
templates/kube-state-metrics/kube-state-metrics-istio-policy.yaml:3:apiVersion: "authentication.istio.io/v1alpha1"
templates/alertmanager/alertmanager-istio-policy.yaml:3:apiVersion: "authentication.istio.io/v1alpha1"
templates/alertmanager/alertmanager-istio-policy.yaml:34:apiVersion: "authentication.istio.io/v1alpha1"
unit-tests/policies/imageFlavor/image_flavor.rego:53:  found_alpha(extra_slice)
unit-tests/policies/imageFlavor/image_flavor.rego:56:found_alpha(x) if {
```

2. Grafana

