VM-cluster

| workload  | section           | Version   |
| --------- | ----------------- | --------- |
| vminsert  | startup Probe     | >= 1.18.0 |
| vmselect  | startup Probe     | >=1.18.0  |
| vmstorage | startup Probe     | >=1.18.0  |
|           | ephemeral storage | >=1.19.0  |

VM-Agent

| workload | section           | Version   |
| -------- | ----------------- | --------- |
| vm-agent | startup Probe     | >= 1.18.0 |
|          | ephemeral storage | >=1.19.0  |

VM-Single

| workload  | section           | Version   |
| --------- | ----------------- | --------- |
| vm-single | startup Probe     | >= 1.18.0 |
|           | ephemeral storage | >=1.19.0  |

VM-alert

| workload | section           | Version   |
| -------- | ----------------- | --------- |
| vm-alert | startup Probe     | >= 1.18.0 |
|          | ephemeral storage | >=1.19.0  |
Gen3GPPXML

| workload   | section               | Version   |
| ---------- | --------------------- | --------- |
| gen3gppxml | selector->matchLabels | >= 1.16.0 |
|            | ephemeral storage     | >=1.19.0  |
Grafana

| workload | section                                | Version   |
| -------- | -------------------------------------- | --------- |
| grafana  | ephemeral storage                      | >= 1.19.0 |
|          | extensions/policy (removed extensions) | <1.16.0   |
|          | ingress hosts                          | <=1.19.0  |

CPRO

| workload        | section                                | Version   |
| --------------- | -------------------------------------- | --------- |
| AM              | selector -> matchLabels                | >= 1.16.0 |
|                 | ingress -> backend                     | <=1.19.0  |
|                 | extensions/Policy (removed extensions) | <1.16.0   |
| KSM             | extensions/Policy (removed extensions) | <1.16.0   |
|                 | selector -> matchLabels                | >= 1.16.0 |
| NE              | selector -> matchLabels                | >= 1.16.0 |
|                 | extensions/Policy (removed extensions) | <1.16.0   |
| PG              | selector -> matchLabels                | >= 1.16.0 |
|                 | ingress -> backend                     | <=1.19.0  |
| RS              | selector -> matchLabels                | >= 1.16.0 |
|                 | ingress -> backend                     | <=1.19.0  |
|                 | extensions/Policy (removed extensions) | <1.16.0   |
| Server          | selector -> matchLabels                | >= 1.16.0 |
|                 | extensions/Policy (removed extensions) | <1.16.0   |
|                 | ingress -> backend                     | <=1.19.0  |
| Webhook4fluentd | selector -> matchLabels                | >= 1.16.0 |


cert-manager