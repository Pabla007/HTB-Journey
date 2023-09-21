To obtain the name of the domain and OS build this is the great command
```
crackmapexec smb 10.10.56.115
```
┌──(root㉿kali)-[~]
└─# crackmapexec smb 10.10.56.115
SMB         10.10.56.115    445    HAVEN-DC         [*] Windows 10.0 Build 17763 x64 (name:HAVEN-DC) (domain:raz0rblack.thm) (signing:True) (SMBv1:False)

Target_Name: RAZ0RBLACK
NetBIOS_Domain_Name: RAZ0RBLACK
NetBIOS_Computer_Name: HAVEN-DC
DNS_Domain_Name: raz0rblack.thm
DNS_Computer_Name: HAVEN-DC.raz0rblack.thm
Domain Sid: S-1-5-21-3403444377-2687699443-13012745


At this point of time i don't think that's it SMB this time my intuition us telling me to look into either rpc or ldaps or even kerbos at this point of time but i will give a smb try before completely ignoring it.

```
User: twilliams
Passwd: roastpotatoes
```

```
User: sbradley
Passwd: hackingakatesting
```
