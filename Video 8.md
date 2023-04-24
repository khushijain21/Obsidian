
Alert Manager 
CNOT -> takes care of notifi - to alarm/slack/email server

for alarm - it goes to calarm - fluentd - log (some flow)

There are 2 types of ALARM
ADAC - automatic detect automatic clear
ADMC - automatic detect manual clear

CPRO scope - is to raise an alarm based on metrics

alerting rules - in PROMETHEUS
most alerting rules is done by prometheus

handled by VM agent in victoria metrics

alerts are sent to ALERT MANAGAER

*client for AM is prometheus* (huh ?)

there exists an evaluation interval 

---

#### Concept of AM

- Grouping - group alerts from instances and send them
- Inhibition: is a concept of suppressing notifications for certain alerts if certain other alerts are already firing.
- Silences : are a straightforward way to simply mute alerts for a given time

**config map reload ??**

---

- Group Interval
- Group Wait
- Receiver
- Receiver Interval

Good Link for difference of above

[What’s the difference between group_interval, group_wait, and repeat_interval? – Robust Perception | Prometheus Monitoring Experts](https://www.robustperception.io/whats-the-difference-between-group_interval-group_wait-and-repeat_interval/)

