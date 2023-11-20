
https://confluence-app.ext.net.nokia.com/pages/viewpage.action?pageId=473383078

https://serverfault.com/questions/817424/how-to-find-out-the-number-of-time-series-stored-in-prometheus-leveldb


https://grafana.com/docs/grafana-cloud/account-management/billing-and-usage/control-prometheus-metrics-usage/usage-analysis-api/


List of active metrics and their cardinalities
```bash
curl -s http://10.32.180.28:31726/api/v1/label/__name__/values \
| jq -r ".data[]" \
| while read metric; do
    count=$(curl -s \
        --data-urlencode 'query=count({__name__="'$metric'"})' \
        --data-urlencode "time=$now" \
        http://10.32.180.28:31726/api/v1/query \
    | jq -r ".data.result[0].value[1]")
    echo "$count $metric"
done
```

```bash
curl -s http://10.32.180.28:31726/api/v1/labels \
| jq -r ".data[]" \
| while read label; do
    count=$(curl -s http://10.32.180.28:31726/api/v1/label/$label/values \
    | jq -r ".data|length")
    echo "$count $label"
  done \
| sort -n
```



Find active  series of given metric 
```bash
curl -s \
    --data-urlencode "query=$metric" \
    --data-urlencode "time=$now" \
    http://10.32.180.28:31726/api/v1/query \
| jq -c ".data.result[].metric"
```
Fetch a list of metric

```
curl -s  http://10.32.180.28:31726/api/v1/label/__name__/values | jq -r ".data[]" | sort >> out.txt
```


| Descriptions                             | TIme |
| ---------------------------------------- | ---- |
| Getting Metric Data, Labels, Time Series | 1d   |
| Evaluate labels and its possible values: | 12d  |
| Excel Sheet Preparation                  | 6D   | 


Preliminary Results:
A curl request to Prometheus in default config lists 1,645 metrics

Automating tool:

| Descriptions                                          | TIme |
| ----------------------------------------------------- | ---- |
| Getting Metric Data, Labels, Time Series              | 1d   |
| Evaluate labels and its possible values:              | 12d  |
| Excel Sheet Preparation                               | 6D   |
| Writing python script/shell script/excel intelligence | 10d (since there are approx 1600 metrics and will require their understanding to add intelligence)     |





Malpe - Train - adventure water sports

