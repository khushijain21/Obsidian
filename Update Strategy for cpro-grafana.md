
#### 1. When Update Strategy is of type OnDelete

```
# There are 2 update strategies available - Rolling Update (default) and OnDelete.
# User can further configure Rolling Updates as required

updateStrategy:  
  type: OnDelete
#  rollingUpdate:
#    partition: 0
```

Step 2: Changing labels/annotations under ```spec.template``` using command 
```bash
k patch sts  roll-cpro-grafana -p '{"spec":{"template":{"metadata":{"labels": {"somerand":"txt"}}}}}' -n khushi
```

Step 3: No changes are reflected and does not trigger a pod restart

Step 4: Delete the pod manually using command

```
kubectl delete pod roll-cpro-grafana-0 -n khushi
```

Step 5: The pod with updated changes comes up

![[Pasted image 20230224143539.png]]

<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>


#### 2. When Update Strategy is of type RollingUpdate

``` yaml
# There are 2 update strategies available - Rolling Update (default) and OnDelete.
# User can further configure Rolling Updates as required

updateStrategy:  
  type: RollingUpdate
#  rollingUpdate:
#    partition: 0
```

Step 2: Changing labels/annotations under ```spec.template``` using command 

```bash
k patch sts  khu-cpro-grafana -p '{"spec":{"template":{"metadata":{"labels":  {"somerand":"txt"}}}}}' -n khushi
```

Step 3: The pod is restarted to reflect the changes

![[Pasted image 20230224143844.png]]
<div style="page-break-after: always;"></div>


#### 3. Backup and Restore Test

- Backup

```bash
helm3 backup -t gra -n khushi -x 10.75.202.87:80/fpm-cbur
```

- Output
```
{
  "apiVersion": "v1",
  "code": 200,
  "details": {},
  "kind": "Status",
  "message": [
    {
      "kind": "BrPolicy",
      "name": "gra-cpro-grafana",
      "reason": "",
      "status": "Success",
      "weight": 0
    }
  ],
  "metadata": {},
  "reason": "",
  "status": "Success"
}
```


- Restore
```
helm3 restore -t gra -n khushi -x 10.75.202.87:80/fpm-cbur
```
- Output
```
{
  "apiVersion": "v1",
  "code": 200,
  "details": {},
  "kind": "Status",
  "message": [
    {
      "kind": "BrPolicy",
      "name": "gra-cpro-grafana",
      "reason": "",
      "status": "Success",
      "weight": 0
    }
  ],
  "metadata": {},
  "reason": "",
  "status": "Success"
}
```

