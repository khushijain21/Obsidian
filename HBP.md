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






![[Pasted image 20230413115037.png]]