

https://grafana.com/docs/grafana/latest/setup-grafana/configure-docker/

Some points noted

- If the customer is using few images to render, we may use a sidecar, but if 100's of alerts are flowing, it may be reasonable to use a separate container.
- The IR requires 16 GB of free memory to work, this may be large memory footprint when scaled for each pod (requires POC)
docker pull grafana/grafana-image-renderer


https://community.grafana.com/t/grafana-image-renderer-performance-tips/102612


https://mattionline.de/grafana-api-export-graph-as-png/

glsa_bbv81N2d4RZ1F6dk9zRIqrmouhtormGe_ded32fb5


curl -u "admin:admin" -k -H "Authorization: Bearer glsa_bbv81N2d4RZ1F6dk9zRIqrmouhtormGe_ded32fb5" 'http://localhost:49153/d/c1804463-cfd7-48f4-9540-40c84499628f/new-dashboard?orgId=1&from=1695105372330&to=1695126972331&viewPanel=4' -o check2.png




for requests sent to 6 panels at once 
![[Pasted image 20230920093228.png]]


![[Pasted image 20230920101826.png]]


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


https://davisonpro.medium.com/securing-node-js-apps-with-ssl-tls-b3570dbf84a5


