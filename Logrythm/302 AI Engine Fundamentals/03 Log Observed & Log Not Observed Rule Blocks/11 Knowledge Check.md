
![[Pasted image 20240607035646.png]]

**How is a traditional Alarm Rule **different from a Log Observed Rule block?****

This AIE Rule Block is very similar to a simple traditional Alarm Rule; however, the ability to combine this block with other blocks in AI Engine Rules makes it much more powerful for detecting threats.



**What must you do to enable your changes after modifying or creating a rule?** **(so that the new rule definition is loaded** **into memory)**

Restart the AI Engine Servers


## Key Takeaways


## Utilizing AI Engine to detect and alert on log activity involves the creation of AI Engine Rules in the AI Engine Rule Wizard.

The most basic of these rules is the _Log Observed Rule_, which operates as a regular alarm rule – it requires only one instance of a log that meets criteria. However, the ability to combine this block with other blocks in AI Engine Rules makes it much more powerful for detecting threats.


<hr>


## Other Rule Block Types can be combined to monitor for expected logs.

The Log Not Observed Compound Rule Block monitors for the absence of a specific, expected log message within the defined time period.

The Log Not Observed Scheduled Rule Block monitors for the observation of an expected log at some specified time interval.


<hr>

## Group By Fields are parsed metadata fields available for selection within each rule block that allow for establishing rule block relationships within a rule.

This relationship is a way for metadata values from one block to be examined by a successive block.

<hr>
## Before AI Engine Rules can be used, they must be enabled, and the AI Engine service must be restarted.

An AI Engine restart is required when a newly created rule is enabled, an existing enabled rule is modified, the _Restart AI Engine Servers_ button in the AI Engine tab becomes clickable, or when the Restart column in the AI Engine tab displays _Needed_.

