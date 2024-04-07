
![[Pasted image 20231119231622.png]]
There is the nothing in the photo that we can use it for ourselves
![[Pasted image 20240407154741.png | 400]]


```
gobuster dir -u http://10.10.10.103 -w /usr/share/wordlists/dirb/common.txt

/aspnet_client        (Status: 301) [Size: 157] [--> http://10.10.10.103/aspnet_client/]
/certenroll           (Status: 301) [Size: 154] [--> http://10.10.10.103/certenroll/]
/certsrv              (Status: 401) [Size: 1293]
/images               (Status: 301) [Size: 150] [--> http://10.10.10.103/images/]
/Images               (Status: 301) [Size: 150] [--> http://10.10.10.103/Images/]
/index.html           (Status: 200) [Size: 60]

```
![[Pasted image 20231119233234.png]]

```
enum4linux -a 10.10.10.103
```

```
Domain Name: HTB                                                             
Domain Sid: S-1-5-21-2379389067-1826974543-3574127760
```
![[Pasted image 20240407160839.png]]


```
http://10.10.10.103/certsrv
```
![[Pasted image 20240407154257.png]]
We need login and password in order to get the initial access so will keep this in mind as well

Will see we can use Sizzle as the username in future if we don't get anything.


```
smbclient -L 10.10.10.103 -U 'anonymous'
```
![[Pasted image 20240407160216.png]]

```
cme smb 10.10.10.103 -u 'anonymous' -p 'anonymous' --shares
```
domain:HTB.LOCAL
sizzle.htb.local

```
kerbrute userenum -d HTB.local --dc 10.10.10.103 userlist.txt -t  100
```

```
2024/04/07 06:48:37 >  [+] VALID USERNAME:       amanda@HTB.local
2024/04/07 06:48:38 >  [+] VALID USERNAME:       guest@HTB.local
2024/04/07 06:48:40 >  [+] VALID USERNAME:       administrator@HTB.local
2024/04/07 06:48:45 >  [+] VALID USERNAME:       Amanda@HTB.local
2024/04/07 06:48:58 >  [+] VALID USERNAME:       sizzle@HTB.local
2024/04/07 06:49:02 >  [+] VALID USERNAME:       Guest@HTB.local
2024/04/07 06:49:02 >  [+] VALID USERNAME:       Administrator@HTB.local
2024/04/07 06:49:15 >  [+] VALID USERNAME:       AMANDA@HTB.local
2024/04/07 06:49:21 >  [+] VALID USERNAME:       sizzler@HTB.local
2024/04/07 06:50:29 >  [+] VALID USERNAME:       GUEST@HTB.local
```
![[Pasted image 20240407162414.png]]

Valid Users
```
amanda@HTB.local
guest@HTB.local
administrator@HTB.local
sizzle@HTB.local
sizzler@HTB.local
```

