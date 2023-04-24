**METRIC TYPE** in Prometheus

- Counter (increases untill prometheus restarts)
- Gauge -- to measure something that changes frequently
- histogram -- to bucketize information
     -- cumulative counter
     -- total sum
- Summary

CONFIGURATION:
- scrape interval - 1min default
- scrape timeout - 10s default
- evalutation interval - 1m default
- external labels - 
- query_log_file - file path to store promQL data
- rule_files - global file path

- scrape_configs: (imp) configure all targets
           job name: 
  scrape interval : overwrite or global paramater
scrape  timeout : ''
 metrics_path: default is /paths - path to scrape metric from
honor_labels
honor timestamps
scheme - http or https
basic_auth  
              -- username
authorization - for authorizating every scrape request
follow-redirects
tls_config : for http targets - should provide tls certificate

discovery mechanisms: 
   -- two are commnonly used in our project
static configs : hardcoded targets

**SERVICE DISCOVERY CONFIGS**
for K8's DS
node - node_name, ID, node_label, node_labelpresent and many more
service
pod 
endpoints 
ingress - path of each ingress target has to be validated

role: 
kubeconfig_file
basic auth:

relabel configs:
    its like a filter - for exp my app name should be = prometheus
any other app name will be droppped
works as a filter

sourve_label:["appname"]
regex: "prometheus"
action= keep

DID not understand relabel configs
metric relabel config??

drop time series -> metric relabel config
drop target -> relabel config


body_size_limit
sample_limit
label_limit : if more than limit then it is treated as failed

label_name_lenght_limit:
label_value_lenght_limit:
target_limit:

Alerting: 
relabel config:
timeout
api_version
path_prefix
scheme: protocol scheme
basic_auth
oauth
tls_config
alertmanager discovery mechanism


Kuberentes SD config (service discovery)

INGRESS
does not work direclty out of the box - not implemented in current cpro chart

There are various SDM's (service discovery mechanism)

what is gossip mechanism ?

Alert Manager evaluation paramaters:
groups:
- name:
rules:
-alert:
exprs - to evaluate

Recording rule -> write a big rule and point it inside the file - for easy of understanding and less longer expression for querying.


REMOTE WRITE -> endpoints to write your samples to
url:
header:
basic_auth
authorization
oauth
tls
queue_config: 

SIMILARLY - REMOTE READ


