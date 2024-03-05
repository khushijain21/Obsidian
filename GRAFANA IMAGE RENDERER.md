

https://grafana.com/docs/grafana/latest/setup-grafana/configure-docker/

Some points noted

- If the customer is using few images to render, we may use a sidecar, but if 100's of alerts are flowing, it may be reasonable to use a separate container.
- The IR requires 16 GB of free memory to work, this may be large memory footprint when scaled for each pod (requires POC)
docker pull grafana/grafana-image-renderer


https://community.grafana.com/t/grafana-image-renderer-performance-tips/102612


https://mattionline.de/grafana-api-export-graph-as-png/

glsa_bbv81N2d4RZ1F6dk9zRIqrmouhtormGe_ded32fb5

glsa_HmEl48wbFhIUitD0v9xI2RIp6KtSdufM_02cc661f

glsa_1eYZc03KVPPSJICr0Sc8FlY3G557T8I6_f6f264c7

curl -u "admin:admin" -k -H "Authorization: Bearer glsa_bbv81N2d4RZ1F6dk9zRIqrmouhtormGe_ded32fb5" 'http://localhost:49153/d/c1804463-cfd7-48f4-9540-40c84499628f/new-dashboard?orgId=1&from=1695105372330&to=1695126972331&viewPanel=4' -o check2.png


vegat jmeter k6

https://community.grafana.com/t/image-rendering-plugin-service-installation-in-kubernetes-environment/41712


https://linuxhandbook.com/docker-container-monitoring/

https://grafana.com/grafana/dashboards/893-main/


![[Pasted image 20230920154211.png]]


![[Pasted image 20230920154247.png]]



| Tasks                                           | Days |
| ----------------------------------------------- | ---- |
| Understanding code to add TLS and Istio support | 6    |
| Building code and Creating a docker image       | 7    |
| Validating image                                | 3    |
| Helm chart changes, HPA, RBAC, PSP changes      | 10   |
| Helm UT                                         | 8    |
| Dimensioning                                    | 3    |
| E2E testing                                     | 4    |
| Documentation                                   |  3    |


TLS, Istio, RBAC, PSP
Helm
Helm UT



- Dockerizing a nodeJS application https://nodejs.org/en/docs/guides/nodejs-docker-webapp


To install grafana Image renderer using docker-compose

```
version: '2'

services:
  grafana:
    image: grafana/grafana:latest
    ports:
      - '3000:3000'
    environment:
      GF_RENDERING_SERVER_URL: http://renderer:8081/render
      GF_RENDERING_CALLBACK_URL: http://grafana:3000/
      GF_LOG_FILTERS: rendering:debug
  renderer:
    image: grafana/grafana-image-renderer:latest
    ports:
      - 8081
```

Notes:
- Grafana renders an image by making an HTTP request to the remote rendering service, which in turn renders the image and returns it back in the HTTP response to Grafana.


https://grafana.com/docs/grafana/latest/setup-grafana/image-rendering/troubleshooting/#certificate-signed-by-internal-certificate-authorities







Set up Mirror git for GIR
	1. HTTPS support --> GIR
	2. TAR file creation
	3. Respective Pipeline
		1. BDH (BDH script update )
		2. Sonarqube 
	4. random secret for auth token



DEV Environment -
- mirror git
- rpm / tar files
- docker image (image : study use rocky8 nano image )
- docker pipeline
- docker validations

HTTPS support
	GIR source code or configuration can be used to change protocol

Configuration required for Grafana and GIR -->GIR and grafana integration

Helm charts + HBP + HPA + TLS + Storage path + Sensitive data + Enable metrics(integration w/ prometheus)

Automation Testcases discussion (Based on above points turnout)
 - check open source CI pipelines 

Documentation

Note: Need confirmation if its required in BVNF or not

https://stackoverflow.com/questions/24162350/requirehttps-vs-requiretls


https://github.com/Davisonpro/nodejs-ssl/blob/master/index.js
https://davisonpro.wordpress.com/tag/nodejs/


as.csc.in@ingka.com








Certificate Issues


https://community.grafana.com/t/certificate-error-with-renderer-docker-image-and-https/74948

```
version: '2'

  

services:

  grafana:

    image: my-custom-grafana:latest

    ports:

      - '3000:3000'

    environment:

      GF_RENDERING_SERVER_URL: https://renderer:8081/render

      GF_RENDERING_CALLBACK_URL: https://grafana:3000/

      GF_LOG_FILTERS: rendering:debug

  renderer:

    image: grafana/grafana-image-renderer:dev-debian

    ports:

      - 8081

    environment:

      - GF_RENDERING_IGNORE_HTTPS_ERRORS= true

      - IGNORE_HTTPS_ERROR= true

      - GF_LOG_FILTERS= rendering:debug
```


glsa_L2AYB1MWNzTZSn4mxHkoNmld8BGKpQIl_6f36bfbc




![[Pasted image 20240207095058.png]]