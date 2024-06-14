### A corroborated AI Engine Rule is a rule that takes inputs from multiple rules and based on the number of those inputs, triggers an AI Engine Event or Alarm.

- Corroborated AI Engine rules normally consume data from other AI Engine Rules.
- A corroborated rule relies on multiple—but different—events occurring at the same time or within the same time period.
- Using a combined set of events reduces the likelihood of false positives and adds greater certainty that the events require investigation, thus reducing alarms and Analyst alarm fatigue.


## Example Characteristics of Ransomware

This example shows the general characteristics of Ransomware and where these behaviors will be used.

These characteristics can then be turned into a corroborated AI Engine rule...

![[Pasted image 20240614091331.png]]

### Example of Corroborated AI Engine Rule

In this example, the top Corroborated Rule (a Unique Value rule) is looking for ransomware. To do this, it consumes AI Engine events from three other rules (two Log Observed Rules and a Threshold Rule).   
  
If the top-level rule sees two or more of these events it will trigger.
![[Pasted image 20240614091410.png]]

