
This is the fourth way that Log Sources can be onboarded within LogRhythm.

## Collect and centrally store specific events from remote computers using Windowed Event Collection (WEC).


## Definition

**Windowed Event Collection (WEC) for windows log collection is an efficient and easy way to collect logs**. This is how Windows does log aggregations. It uses `WinRM` as the method of communication.

Windows Event Collector is a built-in feature of Microsoft’s Windows, that enables you to collect and centrally store specific events from remote computers. It can be configured as a push or pull via Group Policy.

The Event Collector features use Web Services-Management (WS-Man), is supported on Windows XP & 2003 upwards, work for both domain and non-domain joined computers, and can be set up either manually or automatically using GPO. The transmission of logs is authenticated, encrypted, and can use either AD user or Certificate credentials.

![[Pasted image 20240518172533.png]]




## Use Cases for WEC

>**Simplify administration of Windows Log Collection for **Domain Systems**** 

With subscriptions being pushed via GPO, there is no work required when hosts are added/removed from the environment. In other words: once the GPO has been put out there, and a new machine joins the domain or joins the area that the GPO covers, then that configuration is pushed to that machine automatically, and tells the workstation or server: these are types of logs to send and where to send them to.


>[! bug] **Log collection for transient Windows hosts** 
>(Workstations, VDI environments, etc.) No agent installation or log source configuration is required. Logs will be automatically collected without an administrator's intervention.


>****Low bandwidth remote collection**** 

In environments with low network bandwidth, Windows Event Forwarding (or Windows Event Collection) is a great alternative to using RPC since the required bandwidth is significantly less.


>**Environments where remote RPC isn’t possible** 

Windows Event collector only requires a single network port to work, whereas RPC requires multiple.



## Example Architecture

```
WEC can be as simple as a single server or as complicated as the example architecture. **This is an example architecture for Windows Event Forwarding across** **multiple regions.**
```

Note: WEC Servers have limitations for the number of logs they can collect - refer to Microsoft documentation for these.


Note: **Log Source Virtualization templates** are briefly mentioned here, but these will be explained in more depth later in this lesson. 

  
This example architecture requires the use of a Log Source Virtualization Template if not splitting channels (Note: These templates are explained in more depth in a later lesson.):

- If you put all these logs through a single subscription, you'll have Application, System, and Security logs (if you do the main three Windows logs) all coming through the same channel. 
- It will be difficult for LogRhythm to properly parse those because we're looking at a single log source (it would probably come through the security log). So we'd need to create and apply` Log Source Virtualization templates` so that in the same stream of data, we can parse out the separate event logs: parsing out security logs into a security log template, application logs into an application log template, and system logs into a system log template. 
- The same is true if pulling DNS logs or Windows Sysmon - that's another channel that we'd have coming through the same feed, but we'd want to split those out.

![[Pasted image 20240518180315.png]]


## Requirements

>**WEC Requirements:**
- One or more servers must be acting as a subscription manager and log collector.
- All endpoints and subscription managers must have `WinRM` enabled and remotely available through any local firewalls.
- A local (Windows Workgroups) or Domain Group Policy Object (GPO) must be available, specifying the URL for the subscription manager. In other words: where is the machine going to send its logs?
- One or more event log subscriptions.
- NETWORK Service must be part of the Event Readers Group.
    - A GPO to add the NETWORK Service account to the Event Log Readers group.
    - A GPO to set Access Control Lists (ACLs) on all relevant log channels to allow read access by the Event Log Readers Group.

In addition to the correct ACLs and GPOs, the following network ports are required to be open: TCP port 5985 (HTTP) or TCP port 5986 (HTTPS) on any network access control devices.


By default, all log sources will be collected into a single Log Source. It is recommended to split these into separate channels, i.e. to have all Application logs into a WEC Application Log channel.

![[Pasted image 20240518180750.png]]


