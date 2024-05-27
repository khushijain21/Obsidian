Test Case:
- When shared gatewaty is empty and istio is enabled
	  - create new gateway
- When shared gateway is non-empty
	- use shared gateway
- If both shared gateway and new gateway is enabled
    - Use shared gatewaty

How are we attaching our non http gateway to istio_ingress gateway?