
This AIE Rule Block is very similar to a simple traditional Alarm Rule. However, **the ability to combine this block with other blocks in AI Engine Rules makes it much more powerful for detecting threats.**

![[Pasted image 20240607031212.png]]

## Log Observed Rule Blocks

The first AIE Rule Block type, used most often, is the Log Observed Block. 

- The Log Observed Rule Blocks are configured to **monitor for specified criteria found in a single log message, or a number of these same logs occurring within a specified time span.**
- When the criteria defined in the search filter is met, **the Log Observed Rule Block will evaluate to "true" and will trigger any subsequent actions specified in the rule.** 
- These actions could include the compounded application of another AIE Rule Block (compound rules are quite common in AIE), triggering an AIE Event or AIE Alarm, or the initiation of a Smartresponse remediation action.

![[Pasted image 20240607031336.png]]


## Use Case: Windows Service Stopped

You could use a Log Observed Compound Rule Block to detect if a Windows Service were to stop. 

To do this, you would configure the Rule Block to monitor for the **occurrence of a log that contains a service stopped message**.

If the service stop message is observed, AIE could trigger an Event or Alarm to notify of a potential issue.


## Use Case: Impending Attack


You might configure a Log Observed Rule Block to **monitor for SQL Injection data found in Apache or Microsoft IIS transaction logs,** because these logs may indicate an impending attack or compromise of your organization's sensitive corporate data.

- The Log Observed Rule Block could then be combined with another Rule Block configured to monitor for additional log messages that could be used to correlate this assumption of attack.
- If, and when, criteria for both of the Rule Blocks in your AI Engine Rule have been met, the AIE Rule could be configured to **trigger an Alarm, send a notification to administrators, and perform a Smartresponse auto-remediation action to block the attack.**


### **Log Observed: Example Use Case**

Below is an example of a Log Observed Use Case using the template example referenced earlier – **monitoring for a change in Autoruns in Windows****.** Autoruns are normally used to maintain persistence on a Windows Endpoint post-initial compromise.


![[Pasted image 20240607031930.png]]


### **Available Resources:**

Below is a list of some 3rd party Open Source threat tactics and procedure information related to various attack methods. These (external) resources below can provide you with more information related to supporting your Use Case.



