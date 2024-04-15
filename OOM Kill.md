
Test 
- log format should not change
- check logrotate is happening correctly (if taken)

https://prometheus.io/docs/guides/query-log/  - log query to a file


https://nokia.sharepoint.com/:x:/r/sites/csf/domains/fpm/_layouts/15/Doc.aspx?sourcedoc=%7B5EE1F48E-ED6B-49D7-A021-7A705FC01497%7D&file=Unified_Format_Logging_Message_Definition_CLOG19.5.xlsx&action=default&mobileredirect=true&isSPOFile=1&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiI0OS8yNDAyMjkyNDUxNyIsIkhhc0ZlZGVyYXRlZFVzZXIiOmZhbHNlfQ%3D%3D - clog params

https://gerrit.ext.net.nokia.com/gerrit/gitweb?p=CSF-PROMETHEUS.git;a=tree;f=rpmbuild;h=82cba55a5ad9695f20be02689c98a0a5593ae910;hb=refs/heads/rpm - webhook4fluentd


CPRO

will the container start after start-up probe only?
check execV - syscall.execV

Source Code Changes: 
1. Alertmanager, NodeExporter, Prometheus, Pushgateway (uses prom-log)
Source Code Changes: Create a package that provides logger 
 - add multiwriter support (preferred stdout, file)
 - source code UT

2. Webhook4fluentd, ConfigmapReload4cpro (Uses go-kit-log)
- Add multiwrite support
- source code UT

3. Kube state metrics  
-  It supports writing to both file and stderr (will stderr work or do we need stdout?)
  1.  Flags available `--alsologtostderr` `--log_file` `--log_file_max_size`
- Use syscall.Exec to start main process (after checking istio proxy is up)


5. Victoria Metrics (uses slog)
- Add multiwrite support
- source code UT

6. Gen3GPPXML - /var/log 

8. Proftpd - [Proftpd Logging](http://www.proftpd.org/docs/howto/Logging.html#:~:text=By%20default%2C%20proftpd%20will%20log,conf%20configuration) 
- `TransferLog /var/log/proftpd/transfer.log`
- writing to console will not  be there - should check fluentd container

Remove klogrunner binary for unified logging purpose from docker
Docker Image Testing
Chart Changes
Change UT for the same
Automation 
- all logs should be in clog format

Solutions:
Server - Prometheus 
- Prometheus uses promlog and querylog for logging
- Querylog supports logging to a file (Support to writing to console should be added )

Alertmanager:
- Uses Promlog package 

NodeExporter:
-  collector and main package use two different loggers (from promlog only)

KubeStateMetrics
- It supports writing to both file and stderr (will stderr work or do we need stdout?)
  1.  Flags available `--alsologtostderr` `--log_file` `--log_file_max_size`
- Use syscall.Exec to start main process (after checking istio proxy is up)

Pushgateway:
- Uses promlog

webhook4fluentd:
- Uses go-kit-logger 

ConfigReloader4Cpro
- uses go-kit-log

Victoria-Metrics:
- use syscall.execV after sensitive data parsing is complete to have one main process
- Add code for writing to a file and stdout (support multiwriter)



| Workload         | Container            | Scenario                         | Solutions                                                                            |
| ---------------- | -------------------- | -------------------------------- | ------------------------------------------------------------------------------------ |
| Server           | cpro-server          | For Unified Logging              | <br>                                                                                 |
|                  | configmap-reloader   | For Unified Logging              | <br>                                                                                 |
| Alertmanager     | cpro-alertmanager    | For Unified Logging              |                                                                                      |
|                  | configmap-reloader   | For Unified Logging              |                                                                                      |
| nodeexporter     | cpro-nodeexporter    | For Unified Logging              |                                                                                      |
| kubestatemetrics | cpro-ksm             | For Unified Logging, Istio Proxy |                                                                                      |
| pushgateway      | cpro-pushgateway     | For Unified Lo                   |                                                                                      |
| webhook4fluentd  | cpro-webhook4fluentd | UL                               |                                                                                      |
|                  | monitoring container | should check                     |                                                                                      |
|                  | <br>                 |                                  |                                                                                      |
| Gen3GPPXML       | gen3gppxml           | UL<br>                           |                                                                                      |
|                  | configmapreloader    | UL                               |                                                                                      |
|                  | proftpd              | sensitive data & unified logging | startup-probe, init container (for sensitive data)<br><br>flag based for UL          |
|                  |                      |                                  |                                                                                      |
| cpro-vmagent     | vmagent              | UL & sensitive data              |                                                                                      |
|                  | configmapreload      | UL                               |                                                                                      |
|                  |                      |                                  |                                                                                      |
| cpro-vm-cluster  | vminsert             | UL                               | <br>                                                                                 |
|                  | vmselect             | UL                               |                                                                                      |
|                  | vmstorage            | UL<br>                           |                                                                                      |
|                  | backup               | (need to check)                  | same as below                                                                        |
|                  |                      |                                  |                                                                                      |
| cpro-vm-single   | configmapreloader    | UL                               |                                                                                      |
|                  | cpro-vm-single       | UL                               |                                                                                      |
|                  | backup               | (need to check)                  | will be handled by Nihal's contribution<br><br>Chart Changes will be required and UT |
|                  |                      |                                  |                                                                                      |
| cpro-vm-alert    | vmalert              | UL                               |                                                                                      |
|                  | configmapreload      | UL                               |                                                                                      |

- check monitoring container
- if UL is enabled, logs from proftpd container will be visible in fluentd (possible announcement)
- check for fluentd errors (if any) (Unknown)
- add UT to check command args (for any multiprocess) 

Goal:
- No container should start with 2 process
- log format should not change

Prometheus:  
To create module extending promlog (4 days)
UT for Module (2 day) 
(manual) Testing and Validating the module for prometheus (1 day)

Alertmanager, Pushgateway, NodeExporter:
- Source Code changes for all three  - (5 days)
- Manual Testing and Validation - 2 day
- UT for AM, PG, NE - 

Monitoring Container (uses logging module by Python)
- Sample code to log both to a file and console
```
import logging

# Configure logging to file
file_handler = logging.FileHandler('example.log')
file_handler.setLevel(logging.INFO)

# Configure logging to console
console_handler = logging.StreamHandler()
console_handler.setLevel(logging.INFO)

# Set the format for both handlers
formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
file_handler.setFormatter(formatter)
console_handler.setFormatter(formatter)

# Add both handlers to the root logger
logger = logging.getLogger('')
logger.setLevel(logging.INFO)
logger.addHandler(file_handler)
logger.addHandler(console_handler)

# Log messages
logger.debug('This is a debug message')
logger.info('This is an info message')
logger.warning('This is a warning message')
logger.error('This is an error message')
logger.critical('This is a critical message')

```
- Add source code changes - 5 days
- Add UT

Webhook4fluentd, ConfigmapReload4cpro:
- Source Code changes  - 3 days
- UT and manual testing - 2 days

Kube state metrics 
- Remove unified logging logic from klogrun - 1 day
- use syscall.execV function to create a main process - 1 day
- Manual test for klogrun (1 day)
- Code cleanup and modifying UT 2 days for KSM (2 days)

Victoria Metrics (uses slog library) (3 days - source code, 2 days for UT)
- Add multiwrite support (file & console)
- source code UT

Proftpd - [Proftpd Logging](http://www.proftpd.org/docs/howto/Logging.html#:~:text=By%20default%2C%20proftpd%20will%20log,conf%20configuration) 
-  Support file based logging using - `TransferLog /var/log/proftpd/transfer.log` (2 day)
- use syscall.execv for proftpd starter - (including rework and review) (2 days)
- Manual Testing - 1 day

Chart Changes:
CPRO - (includes Monitoring, configmapreload, KSM, NE, AM, PG)
- Remove klogrun binary (5 days)
- Add flags for logging to a file (3 days)
- Add/Modify UT (3 days)

Gen3gppxml & Proftpd
- Chart changes & Manual Validation (1 day)
- Proftpd chart changes - remove klogrun for unified logging (2 days)
- Helm UT (2 day)

Victoria-Metrics
- Remove klogrun binary for sensitive in backup file for vmcluster and vmsingle and related UT (3 days)
- Remove klogrun for unified logging in all 4 charts - 4 days
- Add/Modify UT for all 4 charts (3 days)

Check for fluentd errors if any (for all containers) - 2 days
Pipeline Monitor - 4 days












(Check for only 1 component?)
Automation - 
- Get familiarized w/ automation framework : - 3 days
- Reduce memory size of container - 1 day (for 1 component)
- Check Kubelog 


```
ts=2024-04-04T15:17:33.057Z caller=main.go:521 level=error msg="Error loading config (--config.file=prometheus.yml)" file=/home/khushijain21/prometheus/prometheus.yml err="open prometheus.yml: no such file or directory"
```

