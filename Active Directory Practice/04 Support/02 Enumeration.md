
```
Domain Name: SUPPORT                                                           
Domain Sid: S-1-5-21-1677581083-3380853377-188903654
```

```
 smbclient -L 10.10.11.174 
```
![[Pasted image 20231121141920.png]]


I got the valid user but it tooks some try's to get the domain name right
```
kerbrute userenum -d SUPPORT --dc 10.10.11.174 userlist.txt -t 100
```

```
support@SUPPORT
guest@SUPPORT
administrator@SUPPORT
management@SUPPORT
ldap@SUPPORT
```
![[Pasted image 20231121144103.png]]

