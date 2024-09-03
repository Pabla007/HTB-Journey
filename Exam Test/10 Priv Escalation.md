Now we need to escalate and i will go with what we learn in WPE rather than new approaching and see if the Ninja technique that i learnt is successful.

Will check the location where we can run Powerview
[applocker-bypas-checker.ps1](https://github.com/sparcflow/GibsonBird/blob/master/chapter4/applocker-bypas-checker.ps1)

Whitelist
```
C:\Windows\Tasks
```


So now i was able to run Seatbelt
```
Seatbelt.exe -group=all -full
```
https://github.com/GhostPack/Seatbelt#command-groups


```
Import-Module ./PowerView.ps1
```

```
Get-NetLocalGroup

ComputerName GroupName                           Comment
------------ ---------                           -------
PC-FILESRV01 Access Control Assistance Operators Members of this group can remotely query authorization attributes and permissions for resources on this computer.
PC-FILESRV01 Administrators                      Administrators have complete and unrestricted access to the computer/domain
PC-FILESRV01 Backup Operators                    Backup Operators can override security restrictions for the sole purpose of backing up or restoring files
PC-FILESRV01 Certificate Service DCOM Access     Members of this group are allowed to connect to Certification Authorities in the enterprise
PC-FILESRV01 Cryptographic Operators             Members are authorized to perform cryptographic operations.
PC-FILESRV01 Device Owners                       Members of this group can change system-wide settings.
PC-FILESRV01 Distributed COM Users               Members are allowed to launch, activate and use Distributed COM objects on this machine.
PC-FILESRV01 Event Log Readers                   Members of this group can read event logs from local machine
PC-FILESRV01 Guests                              Guests have the same access as members of the Users group by default, except for the Guest account which is further restricted
PC-FILESRV01 Hyper-V Administrators              Members of this group have complete and unrestricted access to all features of Hyper-V.
PC-FILESRV01 IIS_IUSRS                           Built-in group used by Internet Information Services.
PC-FILESRV01 Network Configuration Operators     Members in this group can have some administrative privileges to manage configuration of networking features
PC-FILESRV01 Performance Log Users               Members of this group may schedule logging of performance counters, enable trace providers, and collect event traces both locally and vi...
PC-FILESRV01 Performance Monitor Users           Members of this group can access performance counter data locally and remotely
PC-FILESRV01 Power Users                         Power Users are included for backwards compatibility and possess limited administrative powers
PC-FILESRV01 Print Operators                     Members can administer printers installed on domain controllers
PC-FILESRV01 RDS Endpoint Servers                Servers in this group run virtual machines and host sessions where users RemoteApp programs and personal virtual desktops run. This grou...
PC-FILESRV01 RDS Management Servers              Servers in this group can perform routine administrative actions on servers running Remote Desktop Services. This group needs to be popu...
PC-FILESRV01 RDS Remote Access Servers           Servers in this group enable users of RemoteApp programs and personal virtual desktops access to these resources. In Internet-facing dep...
PC-FILESRV01 Remote Desktop Users                Members in this group are granted the right to logon remotely
PC-FILESRV01 Remote Management Users             Members of this group can access WMI resources over management protocols (such as WS-Management via the Windows Remote Management servic...
PC-FILESRV01 Replicator                          Supports file replication in a domain
PC-FILESRV01 Storage Replica Administrators      Members of this group have complete and unrestricted access to all features of Storage Replica.
PC-FILESRV01 System Managed Accounts Group       Members of this group are managed by the system.
PC-FILESRV01 Users                               Users are prevented from making accidental or intentional system-wide changes and can run most applications
```




```
PS C:\Windows\Tasks> Get-NetLocalGroupMember


ComputerName : PC-FILESRV01
GroupName    : Administrators
MemberName   : PC-FILESRV01\Administrator
SID          : S-1-5-21-4241685735-4112329853-1893400299-500
IsGroup      : False
IsDomain     : False

ComputerName : PC-FILESRV01
GroupName    : Administrators
MemberName   : HOLOLIVE\Domain Admins
SID          : S-1-5-21-471847105-3603022926-1728018720-512
IsGroup      : True
IsDomain     : True
```



```
PS C:\Windows\Tasks> Get-NetLoggedon


UserName     : watamet
LogonDomain  : HOLOLIVE
AuthDomains  :
LogonServer  : DC-SRV01
ComputerName : localhost

UserName     : PC-FILESRV01$
LogonDomain  : HOLOLIVE
AuthDomains  :
LogonServer  :
ComputerName : localhost

UserName     : PC-FILESRV01$
LogonDomain  : HOLOLIVE
AuthDomains  :
LogonServer  :
ComputerName : localhost

UserName     : PC-FILESRV01$
LogonDomain  : HOLOLIVE
AuthDomains  :
LogonServer  :
ComputerName : localhost

UserName     : PC-FILESRV01$
LogonDomain  : HOLOLIVE
AuthDomains  :
LogonServer  :
ComputerName : localhost

UserName     : PC-FILESRV01$
LogonDomain  : HOLOLIVE
AuthDomains  :
LogonServer  :
ComputerName : localhost

UserName     : PC-FILESRV01$
LogonDomain  : HOLOLIVE
AuthDomains  :
LogonServer  :
ComputerName : localhost
```


```
PS C:\Windows\Tasks> Find-LocalAdminAccess
S-SRV01.holo.live
```


```
PS C:\Windows\Tasks> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== ========
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Disabled
```


![[Pasted image 20240902033528.png]]


