
Grafana docker image runs by default in HTTP mode. We will first bring this in HTTPS mode and then connect remote  image rendering service to it.


We need to create SSL certificate and private key to bring Grafana in HTTPS mode.

The following are openssl commands to do the same. You can run these in an empty folder: 

Change to desired subjectAltName and CN

```
openssl genrsa -out ca.key 2048

openssl req -new -x509 -days 365 -key ca.key -subj "/C=CN/ST=GD/L=SZ/O=Acme, Inc./CN=Acme Root CA" -out ca-crt.pem

openssl req -newkey rsa:2048 -nodes -keyout syslog-key.pem -subj "/C=CN/ST=GD/L=SZ/O=Acme, Inc./CN=*.localhost.com" -out syslog.csr

openssl x509 -req -extfile <(printf "subjectAltName=DNS:localhost,DNS:www.localhost.com") -days 365 -in syslog.csr -CA ca-cert.pem -CAkey ca.key -CAcreateserial -out syslog-cert.pem
```

4.  Set appropriate permissions for the files
```
sudo chmod 400 grafana.key grafana.crt
```

5. Create a *custom.ini* file in the same folder with the following code
```
[server]
http_addr =
http_port = 3000
domain = localhost
root_url = https://localhost:3000
cert_key = /etc/grafana/grafana.key
cert_file = /etc/grafana/grafana.crt
enforce_domain = False
protocol = https

[rendering]
server_url = http://renderer:8081/render
callback_url = https://grafana:3000/

[log]
filters = rendering:debug
``` 

5. We will create a custom docker image from OSS grafana docker. Create a *dockerfile* with the following content

```
FROM grafana/grafana:latest

  
COPY grafana.crt /etc/grafana/grafana.crt
COPY grafana.key /etc/grafana/grafana.key
COPY custom.ini /etc/grafana/grafana.ini
```

6. Build the docker Image
```
docker build -t grafana-custom .
```


7. Create a docker-compose file with the following content

```
version: '2'
  

services:
  grafana:
    image: my-custom-grafana:latest
    ports:
      - '3000:3000'
    environment:
      - GF_RENDERING_SERVER_URL=https://renderer:8081/render
      - GF_RENDERING_CALLBACK_URL=https://grafana:3000/
      - GF_LOG_FILTERS=rendering:debug
  renderer:
    image: grafana/grafana-image-renderer:dev-debian
    ports:
      - 8081
    environment:
       - GF_RENDERING_IGNORE_HTTPS_ERRORS= true
       - IGNORE_HTTPS_ERRORS=true
```

And finally run 
```
docker-compose up
```

And now your Grafana and Graafana image Renderer is up and running

This blog is only a compilation of many sites I had to visit to bring this config up, and may help new users do this quicker. 