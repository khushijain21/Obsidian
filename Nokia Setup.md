https://confluence-app.ext.net.nokia.com/display/CSFDEV/Local+(Laptop)+Working+Guidelines

```
clone_csf

1. chmod 777 clone_csf
2. sudo cp clone_csf /usr/bin
3. clone_csf
```

```
ncs config set --endpoint https://10.76.154.106:8082/ncm/api/v1/  
ncs user login --username=ncs-admin --password=ncs@CPROC3  
export KUBECONFIG=/home/assb/.kube/ncm/config
```