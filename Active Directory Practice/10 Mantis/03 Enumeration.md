
```
Domain Name: HTB                                                              
Domain Sid: S-1-5-21-4220043660-4019079961-2895681657
```

```
kerbrute userenum -d htb.local --dc 10.10.10.52 userlist.txt -t 100
```

```
james@htb.local
James@htb.local
administrator@htb.local
mantis@htb.local
JAMES@htb.local
Administrator@htb.local
Mantis@htb.local
```

![[Pasted image 20240515233953.png]]


We have to go Old School as this machine is hard and we need a entry point to get into.
We have 2 domain controller and 3 http sites which simply means that we have to do directory busting.

```
http://10.10.10.52:1337/secure_notes/
```
![[Pasted image 20240516003001.png]]

We already have the valid user names so in short we have the usernames and all we need is a password to get into.

