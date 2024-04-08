
What can we do with a user name and password
```
prompt off
recurse on
ls
mget *
```
![[Pasted image 20240408013556.png]]

I don't know what's the certificate for now and whether we should generate it or not but will try to do secrets dump and ldapdump 1st.

```
ldapdomaindump ldaps://10.10.10.103 -u 'HTB\Amanda' -p 'Ashare1972'
```
![[Pasted image 20240408014627.png]]

Will run bloodhound on this tomorrow.

It seems like we have to do something with the certificate i guess. Like make a certificate for Amanda.

![[Pasted image 20240408131444.png]]

Will select advanced certificate request as User certificate throughs error at us.
![[Pasted image 20240408131533.png]]

