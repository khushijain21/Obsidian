
generate XML files by querying prometheus

create JSON file
vesAgent: ? minimal functionality

postFix: 1 file for entire scrape interval
(if empty - creates file for all instances or all metrics in one file is possible)

job and instances in PR ?

filter: 
measGroups: metric names

---
A lot of queries from gen3GPPXML - a lot of memory, networy and CPU usage

solution?

PROCESS POOL

QUERY OPTIMIZATION 
	- Query per metric for all instances
	- Query per instance for all the metric (chosen)
	- went from 2.5 min to 20 sec

what is process and thread pool? 

gen3gppxml moved from thread pool to process pool

threadpoolsize: gives thread pool size
misFireGraceTime: (52s) - 