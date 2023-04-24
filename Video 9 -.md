### Zombie exporter
counting zombie process on a node and converts to prometheus understandable style

needs privilige mode to check zombie process
not enabled in openShift node mode

---
### Rest API

to perform CRUD operations on alerts as PR does not do it in house

2 environment
- VCMT - stored in config map -> etcd
- BVNF - stored in etcd

REST API has 2 diff version 
- version1 for BVNF
- version2 for K8's, VCMT


BVNF case :
when a new group is created - it is stored in etcd - everything gets updated there

Rest API talks to API server - gets the config file - makes changes to it - and then K8 picks up on the changes  and LCM events are fired

PROBLEM WITH VCMT- 
when adding alert to vcmt - helm upgrade overwrites the file

swagger? 

---

Short lived jobs pushes its metrics to pushgateway from which PR scrapes its metrics

does not require special priviliges



