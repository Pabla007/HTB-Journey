Domain Name: VULNNET
Domain Sid: S-1-5-21-1405206085-1650434706-76331420
name:VULNNET-BC3TCK1
domain:vulnnet.local
user:enterprise-security
passwd: sand_0873959498

```
smbclient -L 10.10.51.131 -U enterprise-security@vulnnet.local
sand_0873959498
```
![[Pasted image 20230916183633.png]]

Will peak into the Enterprise-share
```
smbclient \\\\10.10.51.131\\Enterprise-Share -U 'enterprise-security' 
sand_0873959498
```

Contents in the file
```
rm -Force C:\Users\Public\Documents\* -ErrorAction SilentlyContinue
```

So will download the file
![[Pasted image 20230916185621.png]]
```
prompt off
recurse on
ls
mget *
```

Let's see if we can edit the code to our advantage and get a reverse shell this time



