
[https://grafana.com/grafana/dashboards/3489-grafana-alert-dashboard/](https://grafana.com/grafana/dashboards/3489-grafana-alert-dashboard/ "https://grafana.com/grafana/dashboards/3489-grafana-alert-dashboard/")


Grafana Dashboard best practices: https://grafana.com/docs/grafana-cloud/visualizations/dashboards/build-dashboards/best-practices/


How to visualize histograms https://grafana.com/blog/2020/06/23/how-to-visualize-prometheus-histograms-in-grafana/

https://grafana.com/blog/2020/04/14/how-histograms-changed-the-game-for-monitoring-time-series-with-prometheus/ - more about histograms from Bjorn Rabenstein

3010:3000 (host port/container port)


1. Alertmanager Cluster metrics: From Grafana for Unified Architect [Re-`use parts of alertmanager dashboard]  
  Maybe something like this : [https://grafana.com/grafana/dashboards/9578-alertmanager/](https://grafana.com/grafana/dashboards/9578-alertmanager/ "https://grafana.com/grafana/dashboards/9578-alertmanager/")  
[https://grafana.com/docs/grafana/latest/alerting/monitor/#metrics-for-alertmanager](https://grafana.com/docs/grafana/latest/alerting/monitor/#metrics-for-alertmanager "https://grafana.com/docs/grafana/latest/alerting/monitor/#metrics-for-alertmanager")  
[https://grafana.com/docs/grafana/latest/alerting/monitor/#metrics-for-alertmanager-in-high-availability-mode](https://grafana.com/docs/grafana/latest/alerting/monitor/#metrics-for-alertmanager-in-high-availability-mode "https://grafana.com/docs/grafana/latest/alerting/monitor/#metrics-for-alertmanager-in-high-availability-mode")  
  
2. Gossip Protocol Related Metrics:  
  Could be found in point 1.  
3. Grafana Unified Alerting performance metrics:   
  Ref: [https://grafana.com/docs/grafana/latest/alerting/monitor/#list-of-available-metrics](https://grafana.com/docs/grafana/latest/alerting/monitor/#list-of-available-metrics "https://grafana.com/docs/grafana/latest/alerting/monitor/#list-of-available-metrics")  
[https://gerrit.ext.net.nokia.com/gerrit/c/CSF/CSF-GRAFANA-MIRROR/+/6461018/2/devenv/docker/ha-test-unified-alerting/grafana/provisioning/dashboards/alerts/overview.json](https://gerrit.ext.net.nokia.com/gerrit/c/CSF/CSF-GRAFANA-MIRROR/+/6461018/2/devenv/docker/ha-test-unified-alerting/grafana/provisioning/dashboards/alerts/overview.json "https://gerrit.ext.net.nokia.com/gerrit/c/csf/csf-grafana-mirror/+/6461018/2/devenv/docker/ha-test-unified-alerting/grafana/provisioning/dashboards/alerts/overview.json")


visualize histograms:
https://grafana.com/blog/2020/06/23/how-to-visualize-prometheus-histograms-in-grafana/



![[Pasted image 20240130150344.png]]

3 instances?

![[Pasted image 20240130150359.png]]