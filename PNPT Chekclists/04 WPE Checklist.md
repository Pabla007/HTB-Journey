

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
whoami /groups
net users
net localgroup
```
 
# Network enumeration
```
ipconfig
route print
arp -a
```
 
# Finding passwords
```
findstr /si password *.txt *.ini *.config
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
```
 
# Services
```
sc query | findstr /B /C:"SERVICE_NAME" /C:"DISPLAY_NAME"
```
 
# Firewall Configuration
```
netsh advfirewall firewall dump
netsh firewall show state
netsh firewall show config
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

