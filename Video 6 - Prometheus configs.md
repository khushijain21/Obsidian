
***own_namespace*** : when it is true service discovery is limited to namespace where prometheus is installed  alone
 
##### REST requests that prometheus provides:
Management API:
Snapshot - to take backup of time series data - POST and PUT is available
skip_head= bool (to take head block or not)
Delete
Tombstone


some endpoints provided by prometheus
```
/api/v1/alerts -> gives us all alerts in json format
```

--- 
ALERTS
GRAPH
STATUS - useful for debugging/ version name/ runtime info
- runtime build info
- TSDB - command line flags/ startup args
- config - all PR configs
- rules
- targets - all targets - if no target is being scraped then job name won't show up ( check in service discovery )
- 

How to create serviceAccount and add rolebinding to them

---

## QUERYING

### Expression language data types[](https://prometheus.io/docs/prometheus/latest/querying/basics/#expression-language-data-types)
In Prometheus's expression language, an expression or sub-expression can evaluate to one of four types:

-   **Instant vector** - a set of time series containing a single sample for each time series, all sharing the same timestamp
-   **Range vector** - a set of time series containing a range of data points over time for each time series
-   **Scalar** - a simple numeric floating point value
-   **String** - a simple string value; currently unused


USEFUL LINK  - [Querying basics | Prometheus](https://prometheus.io/docs/prometheus/latest/querying/basics/)

---

### FEDERATION

- Hierarchical fed
- Cross - service fed

---
### How data is stored

HEAD CHUNK -> 120 samples - is in memory before persists later into disk

XOR encoding is done to compress the head chunk from 16 bytes to 1.3 bytes

What happens when process crashes - to solve it, we use WAL (write ahead log)

checkpoints are created from where data is replayed

2/3rd of WAL is checkpointed

**TRUNCATION and COMPACTION**

Head Block consists of many chunks - > which gets truncated, compacted and then stores on disk

#### tombstone ??

truncation -> compaction -> checkpointing

headchunk -> chunk -> headblock -> block

after chunks is stored on disk - it is removed from WAL

BUTTTTTTTTT massive optimization is possible and we see that ahead 

---
OPTIMIZING MEMORY IN PROMETHEUS

chunk is sent to disk - its meta data is still in head block

snapshot during shutdown - a feature that will help crashed prometheus restart faster

---
### Dimensioning

what resources should you dimension
- cpu
- ram
	- Headblock
	- Indexes, labels, tombstones
	- Loading Additional blocks based on the query
- disk
	- WAL
	- head chunks, blocks, snapshot

---
#### Monitoring


---
#### Sharding

if you want to scale PR - with sharded environments - then both PR should be queried so that Grafana can get a global view

currently not used in CPRO

---
#### Security

Some vulnerabilities exists - is sent to community to fix it when found

No authentication in PR but single sign on exists

---
What is multitenancy? / performance benchmarking / 

---
K8's RBAC
PSP -> pod security policy - defines what the pod can do like privilige escalation, read, write, delete etc

different from role because role is defined for others on what they can do with the pod

Prometheus scrapes for entire cluster or it can be restricted to a single namepsace by providing role and rolebinding

Currently support for only single namespace

```
kubectl auth can-i get pods
```







