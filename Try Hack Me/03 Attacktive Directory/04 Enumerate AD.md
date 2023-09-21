Port that comes to ones mind after seeing the nmap scan 
88      Kerberos for authentication purpose
139/445 SMB
3268    ldap

Target_Name: THM-AD
NetBIOS_Domain_Name: THM-AD
NetBIOS_Computer_Name: ATTACKTIVEDIREC
DNS_Domain_Name: spookysec.local
DNS_Computer_Name: AttacktiveDirectory.spookysec.local

 Message signing enabled and required

Here i am using a new tool for enumerating SMB 139/445 as earlier i was using smbclient or Metasploit aka msfconsole

But here will use enum4linux
https://www.kali.org/tools/enum4linux/

```
 enum4linux -U -o 10.10.148.33
```

![[Pasted image 20230912232212.png]]

Target ........... 10.10.148.33
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none

Domain Name: THM-AD
Domain Sid: S-1-5-21-3591857110-2884097990-301047963

What is TLD 
![[Pasted image 20230912232817.png]]


