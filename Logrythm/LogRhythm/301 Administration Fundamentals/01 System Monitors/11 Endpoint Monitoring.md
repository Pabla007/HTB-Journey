
**System Monitors are capable of monitoring several aspects of an endpoint**, including user activity, system processes, and network connections.

Most of the features are available on the Lite System Monitor license, with one exception. Registry Integrity Monitoring (RIM) is available only on Windows Pro licensed System Monitors.

In most cases, each feature needs only to be enabled to begin collecting information. For File Integrity Monitoring (FIM), Registry Integrity Monitoring (RIM), and Data Loss Defender (DLD) additional configuration is required (discussed in the topics below). 

See below for details about:

1. User Activity Monitoring
2. Registry Integrity Monitoring (Windows Only)
3. Data Loss Defender (External Media)
4. File Integrity Monitoring
5. The Network Connection Monitor (Socket Connections)
6. The Process Monitor  
      
    *These features are License Type and OS dependent.  
    Linux does not include Registry Integrity Monitoring. And a Light License does not include File Integrity Monitoring, Registry Integrity Monitoring, or Data Loss Defender.



## User Activity Monitoring (UAM) 
is employed by each of the endpoint monitoring options. 

User Activity tracks who's logging in and who's logging out, independent of the Windows or operating system who is logging in and out. `The Agent can see it before the operating system does!`

  
UAM settings are located within the User Activity Monitor tab under the Endpoint Monitoring settings in the System Monitor Agent Properties window.


User Activity Monitoring must be enabled before it can be used by the other endpoint monitors. If enabled, the System Monitor will generate information when any user launches or kills a process, accesses/creates/deletes a file, opens/closes network connections, and performs any log on/log off activity.

  
User Activity Monitoring must be enabled on the User Activity Monitoring sub-tab, under the Endpoint Monitoring tab of a System Monitor for log on, process, and network connection activities.

 ![[Pasted image 20240515151514.png]] 
**Important:** User Activity Monitoring does come with a cost – it will add additional CPU and memory overhead to the host when it is enabled. Also, to note, LogRhythm’s sizing recommendations are based on endpoint monitoring being turned off.


##  Registry Integrity Monitoring

**Windows registry keys contain important information necessary to the operation of the Windows OS.**

These keys can be monitored to ensure they have not been modified.

Registry Integrity Monitoring (RIM) functions much like Realtime FIM. You must define a policy that defines the Windows registry keys to monitor. The policy can be assigned to a Windows Pro licensed System Monitor to monitor the local Windows Registry files.


RIM is always a Realtime monitoring function. You simply define which registry keys to monitor, and RIM will monitor for any changes made to that key or any recursive keys.

![[Pasted image 20240515151448.png]]


##  Data Loss Defender

**Data Loss Defender (DLD) monitors activity on a host's CD/DVD, USB, and Flash drives.** It will monitor for CDs or DVDs inserted into a drive and for any memory devices (USBs, flash drives, hard disk drives, cell phones, etc.) inserted into any of the USB ports on a host. If DLD detects one of these activities, it can also eject the device or prevent the device from mounting and becoming available to the operating system.

**Data Loss Defender Policies**

The DLD Monitor requires a configuration policy prior to enabling. The DLD policy only contains the following options:

- USB/Flash Drives
    - Monitor
    - Eject
- CD/DVD Drive
    - Monitor
    - Eject


![[Pasted image 20240515151905.png]]


## File Integrity Monitor

**File Integrity Monitoring (FIM) will monitor files and directories specified by one or more FIM Policies for modifications to:
•    File reads
•    File contents
•    File permissions
•    File Access Control Lists (ACL)
  

FIM allows for monitoring in two modes:
•    Realtime monitoring (on Windows and some Linux systems)
•    Standard monitoring (on Windows and Linux)


**File Integrity Monitor Policies**

FIM Polices can be created and edited using the File Integrity Monitor Policy Manager, found in the Tools - Administration menu in the Client Console.

Default FIM policies are provided for common operating systems such as Windows. The default policies define common Windows and UNIX files and directories.

  
Each FIM policy contains configurations for the files and directories to monitor, the maximum file size, and the schedule for monitoring. Each of these configuration options are for Standard Mode FIM, whereas Realtime Mode FIM uses only the file and directory definitions.


**See below for more details about how FIM works.**
![[Pasted image 20240515152657.png]]


## Administration from the Deployment Manager

Registry Integrity Monitoring, Data Loss Defender, and File Integrity Monitor do have policy managers that can be managed from Deployment Manager > Tools > Administration. See the image below to see how to access those.

![[Pasted image 20240515152820.png | 500]]

## Network Connection Monitor

**Network connections** can be independently monitored for network connections being opened and closed on a Windows or UNIX host.

The System Monitor will generate a log when a connection opens on the host and another log when it detects that the connection has been closed. If enabled, the Network Connection Monitor logs will contain UAM information about the users connected to the host at the time the connection was opened or closed.  

Logs include, but are not limited to, the following data:

- Protocol
- Local IP address and port
- Remote IP address and port
- Open time and close time
- Duration

The Network Connection Monitor can be enabled to monitor:

- Inbound TCP connections
- Outbound TCP connections
- Listening TCP/UDP sockets

![[Pasted image 20240515154720.png]]


##  Process Monitor

**Process monito****ring logs when processes start and stop** on a Windows or UNIX host running a System Monitor. The System Monitor generates a log when a process starts on the host and another log when the System Monitor detects the process has stopped. 

If enabled, the Process Monitor logs will contain UAM information about the users connected to the host at the time the process was started or stopped.

Log messages include but are not limited to:
- Process name
- Owner name
- Start time
- Duration

Network Connection Monitor
![[Pasted image 20240515154935.png]]


