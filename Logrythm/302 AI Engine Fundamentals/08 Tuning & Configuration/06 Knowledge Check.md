
Read each question and make a guess. Then flip the flashcard to view the answer.

**Why are corroborated rules helpful?**

A corroborated rule relies on multiple, but different events occurring at the same time or within the same time period. This adds greater certainty that the events require investigation.




**Why are "Workloads" helpful?**

Workloads allow Administrators to load rules into the AI Engine. They allow Administrators to choose **only** the rules they actually intend to use. This reduces the memory required to load rules and saves processing power.




**Why should you not enable every rule in an AI Engine arsenal?**   
  
**Similarly, why should you limit Log Source Criteria for AIE Rules to applicable log sources only?**


**It can cause excessive resource consumption and taxation.**

- Every AIE Rule carries a certain level of processing and memory requirements.
- It is unlikely that AI Engine will require monitoring _all_ logs from _all_ devices for _all_ rules – many logs will never meet rule criteria. 
- Log Source Criteria is examined per rule block, not per rule. If Log Source Criteria for every AIE Rule includes all log sources, multiple instances of this criteria will be present for multi-block AIE Rules.


### Key Takeaways

## Corroborated AI Engine Rules are rules that rely on multiple, but different AIE Rule inputs to occur within the same time period, generating AI Engine Events or Alarms based on these inputs.

Corroborated rules reduce the probability of false positives by decreasing the likelihood that an Event is an anomaly or coincidental.


## To maximize rule performance and platform stability...

...it is important to not enable every AI Engine Rule and to limit Log Source Criteria to _applicable_ log sources only, where possible.


## A Workload is an AI Engine Rule container that specifies rules available for use by a given AIE server.

Workloads can be used to further tune AI Engine by providing a way for metadata to be inspected prior to reaching the AI Engine Service. In other words, they act as a filter between the AI Engine Comms Manager and the Data Processor.