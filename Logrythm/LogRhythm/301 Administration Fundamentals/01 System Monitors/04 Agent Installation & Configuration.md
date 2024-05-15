
##  Windows & *Nix OS distributions

>[! question] LogRhythm offers two types of installations: Windows and *NIX.  
  
**For Windows Installation:**

- 32-bit and 64-bit platforms are supported. 
    - If you run Core platforms, such as a Windows server without a desktop interface, LogRhythm also has Agents for Core: 64-bit Core. 


>[! bug] All these require .NET 4.7.2 or above to be installed on the machine. The Agent won't install unless it is there.
    - Ensure you have the correct platform!


- Initial Agent Configuration takes place in the Configuration Manager application.
- Windows packages can even be deployed silently (pushed to machines remotely and installed without interaction).

**For *NIX Installation:**

- Supported on various distributions (e.g. CentOS/RHEL, SUSE, Ubuntu, etc.).
- Initial Agent configuration takes place within specified configuration files (scsm.ini).
- Linux instructions are available as a separate download, alongside Agent downloads.
    - Instructions will contain prerequisite information and additional steps for installing, upgrading, or removing Agents.


## Installation Packages & Guides

**Reference LogRhythm Community Documentation**  
Before installing a new Agent, it is recommended that you reference documentation on LogRhythm Community.  
  
LogRhythm provides installation packages and installation guides for the various platforms.


![[Pasted image 20240514143243.png]]


## Data Processor

**Regardless of platform, each Agent must be configured to communicate with a Data Processor for log delivery.**

Installing the System Monitor Agent requires that the settings for the initial Data Processor be configured. This configuration is performed on the System Monitor Configuration Manager (in Windows) or via the `scsm.ini` file on *Nix systems located in the System Monitor's config directory, typically found in `/opt/LogRhythm`

For each configuration option, the Agent will report to a single Data Processor; however, it can be configured to have two backup Data Processors in case the primary goes offline or is otherwise unavailable.

![[Pasted image 20240514143941.png]]



## Local Agent IP Address

The Agent does require that the **local System Monitor IP address be set** as well. While this setting can use an index value for its IP address, using the index value (0 by default) is not recommended on all systems. Use of the index value may return a local IP address of 127.0.0.1 (the loopback address) that would prevent the System Monitor from communicating.

![[Pasted image 20240514144153.png]]



