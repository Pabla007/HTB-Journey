
The Log Not Observed Compound Rule Block **monitors for the absence of a specific log message within the defined time period**.

**Log Not Observed Compound Rule Block**

![[Pasted image 20240607032250.png]]

1. **You'll use this block to look for data you are expecting to see.** When the expected data is not observed, it could indicate a failure or other issues.
    
2. The Log Not Observed Compound Rule Block **requires that it is combined with another Rule Block**. 
    
    - The first Rule Block **must be evaluated to true** before AIE will execute this compound Rule Block. 
    - AIE uses the preceding block as a boundary for this block’s execution, otherwise its execution would be arbitrary and cause false positives.


>[!bug ] **Troubleshooting a Log Not Observed Rule requires resolution at the log source level since the rule inherently relies on the absence of log data.**

## Use Case: Stopped Windows Service Fails to Restart

You could use a Log Not Observed Compound Rule Block after a Log Observed Block to detect if a Windows Service were to stop then fail to restart:

- You could configure **the first block** to monitor for the occurrence of a log that contains a service stopped message. 
- After this log is observed, **the second block** would be executed to monitor for the expected log that contains a service started message. 
- If the service start message is not observed within your specified time range, perhaps five minutes, **AIE could trigger an Event or Alarm to notify of a potential operational issue.**
    - Example: Log Observed = Service Stopped → Log Not Observed = Service Started within 5 Minutes

