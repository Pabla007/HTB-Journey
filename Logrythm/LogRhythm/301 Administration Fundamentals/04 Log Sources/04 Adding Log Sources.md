
```
Log Sources can be added via:
```

![[Pasted image 20240522143742.png]]



## Pending Log Sources

As described in the previous section, network equipment such as firewalls, routers, and switches may generate a Syslog feed when Syslog traffic is pointed to the IP address of a System Monitor Agent.  

When this traffic is detected, the device generating the traffic appears as a pending log source within the Log Sources tab of the Deployment Manager. At this point, the Syslog feed of the device can be accepted as a log source and added into the System Monitor configuration.


## Manual Creation via SMA

Another way to add new Log Sources is from the System Monitor Agent Properties window of the System Monitor that will be collecting the logs. Log Sources that require you to enter customized information must be added from within the System Monitor tab in the Client Console.  

Types of logs that require custom configuration for the System Monitor include flat files, UDLA, or any other Log Source that requires the use of an API (application programming interface) for collection of logs.

**How to:**  

To add a new Log Source, double-click an active System Monitor listed in the System Monitors tab of the Deployment Manager. This opens the System Monitor Agent Properties window.
 

Located at the bottom of this properties window is a table of Log Sources from which this System Monitor will be collecting log messages. Right-click within this table and select New to begin the process of adding a new Log Source for collection by the System Monitor.
  

Notice the Log Message Source Type and Log Message Source Name fields - certain log source types can enable or disable the Flat File Settings tab.


