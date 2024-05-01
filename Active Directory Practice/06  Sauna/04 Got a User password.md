
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


