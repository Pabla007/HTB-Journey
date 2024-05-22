
```
Log Source Virtualization makes it possible to consume all the available intelligence within a single log stream that contains multiple records from different sources.
```


WHAT & WHY

Log Source Virtualization Templates are required for forwarded/aggregated log sources.

- If collecting from a source that contains different log sources, (e.g. Windows Event Forwarding, Syslog Relay, or Single Channel Source), a Log Source Virtualization template is required. 
- This helps ensure that the Log Messages from the varying log source types are processed correctly.


<hr>


HOW THEY WORK

NEW LOG SOURCE VIRTUALIZATION EXAMPLE

**When virtualization is enabled on a log source, it is referred to as a “parent” log source**, and the different records inside it are referred to as either “virtual” or “child” log sources (when referencing log sources, the terms “virtual” and “child” are often used interchangeably).

  

**Virtual log sources are treated in the same way as other log sources.** They are processed in accordance with their assigned Message Processing Engine (MPE) policies, and they appear in the same lists as the other log sources within the deployment. 

  

**Log Source Virtualization can be applied broadly.**  Log Source Virtualization can be applied to syslog relay sources, Windows Event Logs, flat files, and any other log source within your deployment that contains multiple records. This is different from Syslog Virtualization, which applies only to syslog relay logs received by the System Monitor syslog server. 

  

**If using Open Collector**, an LSV template provided via the Knowledge Base Manager is needed.

  

To learn more about LSV, go to [LogRhythm Docs(opens in a new tab)](http://docs.logrhythm.com/) > LogRhythm SIEM > Client Console Administrator Guide > Log Sources > Log Source Virtualization.

![[Pasted image 20240522135442.png]]

