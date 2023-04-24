### Kube state metrics
is a services that talks to API server and gets metric of k8 API resources

TOPICS:
collector - namespace scope
collectors - namespace scope
auto sharding
sharding
dimensioning
generic rule alerts
recording rules
Istio config

gives metrics of K8 underlying resources 

Collectors exist for
- objects at cluster level
- objects at namespace level

FLAGS
- alsologtostderr : log to stderr or file
- apiserver - can configure API or default from config file
- enable-gzip-encoding
- host - where to listen to | default listens on every port
and many more
- namepsace - collect metrics from all objects from the given ns
- pod - 
- sharding - create instances of KSM to manage large cluster
- tls-config
- use-apiserver-cache

---
NodeExporter

converts scraped metrics to TSDB format that PR understands

k exec node_exporter -- /bin/node_exporter --help


***timex*** collector -> requires an additon docker

---

Mutator Observer

