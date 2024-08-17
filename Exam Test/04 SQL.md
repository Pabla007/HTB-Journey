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

