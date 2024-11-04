
```
http://10.10.11.108/
```
![[Pasted image 20231122131647.png]]

```
Domain Name: RETURN                                                                                  
Domain Sid: S-1-5-21-3750359090-2939318659-876128439
```


```
svc-printer
Password23!
```
![[Pasted image 20231122135338.png]]

Got a domain dump
```
ldapdomaindump ldap://10.10.11.108
```
![[Pasted image 20231123110200.png]]

It seems like we have to send that user password to us instead let's fireup a netcat listener and see if the data is send to us or not.

Note we have to use the port 389 otherwise the data will not be send to us
The site got hung up that means the data is being send to us.
```
svc-printer
1edFg43012!!
```
![[Pasted image 20231123112124.png]]
![[Pasted image 20231123112040.png]]