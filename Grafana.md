
livenessProbe:
readinessProbe:


HOOKS 

scheme
protocol
certManager

$ kubectl get secret --namespace khushi khu-cpro-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

How to set HA in grafana chart