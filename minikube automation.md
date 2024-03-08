
minikube delete  
minikube config set memory 6144    --> to keep your WSL stable  
minikube config set cpus 3 -->  to keep your WSL stable..    
minikube start \ 
  --kubernetes-version=v1.27.11 \  
  --nodes=3 \  
  --registry-mirror=[https://registry1-docker-io.repo.cci.nokia.net](https://registry1-docker-io.repo.cci.nokia.net "https://registry1-docker-io.repo.cci.nokia.net/") \  
  --registry-mirror=[https://quayio.repo.cci.nokia.net](https://quayio.repo.cci.nokia.net "https://quayio.repo.cci.nokia.net/") \  
  --registry-mirror=[https://gcr-io.repo.cci.nokia.net](https://gcr-io.repo.cci.nokia.net "https://gcr-io.repo.cci.nokia.net/") \  
  --registry-mirror=[https://github-container-registry.repo.cci.nokia.net](https://github-container-registry.repo.cci.nokia.net "https://github-container-registry.repo.cci.nokia.net/") \  
  --registry-mirror=[https://k8s-gcr-io.repo.cci.nokia.net](https://k8s-gcr-io.repo.cci.nokia.net "https://k8s-gcr-io.repo.cci.nokia.net/")

Install Certmanager
```
helm repo add jetstack https://charts.jetstack.io --force-update
```

```
helm repo update
```


Install Ingress

