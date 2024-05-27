
```
An investigative approach in key areas generally leads to faster resolution.
```


It may become necessary to examine log collection issues, as log sources are initially brought in or after log messages have been delivered for some time. Issues may surface from varying connectivity issues, fluctuations in log volume, or as a result of system or permission changes.

The following is an example of an issue with log collection where a log source was successfully brought in but began to reflect increasingly delayed time stamps in the Last Log Message column.


## **Scenario:**

A log source has checked in but has fallen further behind in Last Log Message timestamps, despite continued connectivity and stability of the source.


![[Pasted image 20240528012434.png]]


 **To begin, there are several areas that can be inspected:**

**smcs.log**

The scsm.log is the log file of the System Monitor Agent, located in the Agent’s installation directory. This file will not only display the diagnostic state of the Agent itself but will also display connectivity attempt information for all log sources it is responsible for collecting from (when set to the appropriate logging level).

![[Pasted image 20240528012949.png]]



**Max Message Count**

Every log source within LogRhythm has specific property settings that can be accessed by double-clicking the log source and clicking the **Advanced** **button**, located at the bottom left of the properties window.


In these advanced settings, a value of **MaxMessageCount** can be found. **MaxMessageCount** is the **maximum number of logs that can be collected by a System Monitor per cycle** (known as the Cycle Time of the Agent), with the default being 100 messages for all log sources.


![[Pasted image 20240528013314.png]]

