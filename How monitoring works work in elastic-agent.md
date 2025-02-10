
### How agent.monitoring works in elastic-agent

Monitoring helps us to self monitor the logs and metrics of elastic-agent and its sub processes.
For a config as simple as this, agent internally spawns filebeat and metricbeat to collect logs and metrics respectively. 

```
outputs:
	default:
	type: elasticsearch
	hosts: ["http://localhost:9200"]
	username: elastic
	password: password
	preset: balanced


agent.monitoring:
	enabled: true
	logs: true
	metrics: true
	metrics_period: 60s
	use_output: default
```

---


When `agent.monitoring.logs` is true, a filebeat process is created with following inputs
- a filestream input to monitor agent logs
- a filestream input for service components that define a log path
- Code Ref: [injectLogsInput](https://github.com/khushijain21/elastic-agent/blob/main/internal/pkg/agent/application/monitoring/v1_monitor.go#L317)
	   
 
When `agent.monitoring.metrics:true`,  2 metricbeat instances are created
- One metricbeat with following inputs using the beat module
  <img width="682" alt="Pasted image 20250206135553" src="https://github.com/user-attachments/assets/eaa4710a-de2e-47e8-906a-0644d5513af6" />
        
- Another with the following inputs using the http module
  <img width="947" alt="Pasted image 20250206135519" src="https://github.com/user-attachments/assets/ec744ebd-e5c5-482f-a0be-51c5f49cff99" />  


Any additonal inputs run by elastic-agent are also appropriately added to this list. Note: this diagram is for when no inputs are configured and only `agent.monitoring` is enabled. 

Code Ref: [injectMetricsInput](https://github.com/khushijain21/elastic-agent/blob/main/internal/pkg/agent/application/monitoring/v1_monitor.go#L553)





