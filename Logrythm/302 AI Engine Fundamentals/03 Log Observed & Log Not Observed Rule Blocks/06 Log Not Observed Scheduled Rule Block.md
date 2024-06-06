
The Log Not Observed Scheduled Rule Block monitors for the **observation of an expected log at some specified time interval**.


## The Log Not Observed Scheduled Rule Block

The Log Not Observed Scheduled Rule Block monitors for the observation of an expected log at some specified time interval. If AIE observes this log message, all is well, and no action is triggered. If the log is not observed during the expected time schedule, **AIE can trigger a new Event or Alarm to notify that an expected task was not observed as scheduled.**

Keep in mind, a Log Not Observed is looking for the absence of data, therefore, to troubleshoot this rule, you will need to look at the logs from the endpoint server.

![[Pasted image 20240607033226.png]]


## Must be the ONLY Rule Block in a Rule

The Log Not Observed Scheduled block must be the only rule block. If another rule block is in the designer, you will not be able to add a Log Not Observed Scheduled block to the designer. 


The example below demonstrates what happens when you drag a log observed rule block onto the Rule Designer: the Log Not Observed rule block is greyed out. 


Cancel the Log Observed Block in the example below and the Not Observed Compound rule block would be greyed out instead. The AI Engine Rule Block Designer will dynamically update based on Rule block creation rules.


![[Pasted image 20240607033409.png]]


## Use Case: Backup Job Not Completed at Scheduled Time

In this use case, a Log Not Observed Scheduled Rule Block could be configured to monitor for a log containing a backup completed message during a specified time range every night. If AIE does not observe the log message indicating that the backup process was successful and complete, an Event and Alarm could be triggered to notify of the backup failure. This advanced warning might allow your staff to retry the backup during the night.


