
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
