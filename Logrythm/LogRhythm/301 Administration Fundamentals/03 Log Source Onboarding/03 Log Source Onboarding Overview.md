
```
Log Source Onboarding is the process of accepting logs from different devices on your network.
```


There are various ways of collecting a log source and the methods you use will depend on your environment. See below for each log source onboarding type:

![[Pasted image 20240518170703.png]]


## 1 - Automatic Log Source Acceptance

**For Syslog and Flow Data, which allows for automatic identification and acceptance for Syslog and Flow Data.**  

- Automatic Log Source Acceptance allows the automatic creation of a Log Source Host, Log Source Type, and acceptance of the Log Source. 
- This starts the process of collection nearly immediately.
- Configure it using an IP address range or a regex filter to determine the Log Source Type.
- Your administration time is considerably reduced, by enabling LogRhythm to automatically determine the Log Source Type and accept the Log Source that is collected via Syslog, Flow, and SNMP Trap Receiver.


## 2 - Windows Host Wizard

**Will add multiple log source Types at once for a single host.**

>Windows hosts and Windows Event Log type Log Sources can be added using the Windows Host Wizard. The Windows Host Wizard can be run in a manual mode, allowing you to quickly add Host records and Log Sources using a few pieces of host identity information.


 >[! note] **The Windows Host Wizard is the recommended method for configuring LogRhythm to collect Windows Event Logs.** These logs are collected by a Windows System Monitor.

>A System Monitor collects Windows Event Logs from the host that it is installed on, and it can, depending on the configuration, collect Windows Event Logs from designated remote hosts. One System Monitor can remotely collect from several Windows hosts.



>The Windows Host Wizard is also Active Directory (AD) enabled, which means that you have the option to scan domains for computers (Active Directory Discovery), then import computers (all or some) that are found.


- For the AD Discovery to function, the LogRhythm appliance must be a member of a domain, and credentials must be provided with access to browse AD.
    
    - For example: LogRhythm allows you to put in a Service Account, which is a least-privileged account. It just needs to be able to read AD, not write anything.



## 3 - Manual Local & Remote Log Collection (Flat File)

**Local or Remote manual collection of Flat File log sources via SMB.**

- For Local Collection, the System Monitor Agent resides on the local host. For logs to be remotely collected, the System Monitor must be running under a Windows Service Account that has permissions to connect to and collect Windows Event Log information from these hosts.
- By default, a System Monitor uses the Local System account or a named service account, which may not have permissions on a remote host, i.e. an endpoint that is not domain joined. It is possible within the Host record to specify a local account on the host to be used for collection (if that host is not a domain member).  

![[Pasted image 20240518172007.png]]


