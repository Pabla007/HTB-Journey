
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


![[Pasted image 20240523164104.png]]



## Adding Log Sources from a File

Adding log sources from a file is referred to as Log Source Preregistration and is useful for importing log sources in bulk, especially at the beginning of a deployment.  

You can quickly and easily add Log Sources in bulk from a list in a CSV (comma-separated values) file. This is a good way to pre-register Log Sources and then accept a few at a time, as time allows or as your organization is prepared.

The CSV file must contain at least the IP address, and the import tool in LogRhythm will walk you through the rest. A CSV file can also contain the following information (in the order specified):

- Log Host IP address (required)
- Log Entity
- Log Source Type
- Collection Host (the System Monitor Agent name, not the name containing the Entity and Host as shown in the Collection Host column in Log Sources)
- MPE Policy
- File Path

You can include up to 50,000 Log Sources in one CSV file. Save the file somewhere accessible to the Client Console.

  

**How to:**

To begin the import process, open the Log Sources tab. Right-click in the space at the bottom of your existing Log Sources and select Add Log Sources from File. 

Choose the file location and a preview window will display what was imported. The Status column will show you whether your imported Log Sources are ready to be registered (Valid) or if they are missing data (Invalid).


The entries will display “Invalid” if information is in the wrong field or does not match what LogRhythm is expecting (for example, the Log Source Type you entered doesn't exactly match). If you have Invalid entries, double-click on the entry to select any missing settings.

The Import screen will give you the option to Accept Valid Log Sources.
  

The Valid Log Sources will be removed from the list and added to the Log Sources tab to await the first collected log. Once a log has come in from that source, it will automatically start collecting with no further intervention.



![[Pasted image 20240523164807.png]]

![[Pasted image 20240523164900.png]]

![[Pasted image 20240523164944.png]]

