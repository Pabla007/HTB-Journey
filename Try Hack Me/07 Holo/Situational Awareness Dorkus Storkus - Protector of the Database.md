
```
<?php

define('DB_SRV', '192.168.100.1');
define('DB_PASSWD', "!123SecureAdminDashboard321!");
define('DB_USER', 'admin');
define('DB_NAME', 'DashboardDB');

$connection = mysqli_connect(DB_SRV, DB_USER, DB_PASSWD, DB_NAME);

if($connection == false){

        die("Error: Connection to Database could not be made." . mysqli_connect_error());
}
?>
```


Now will try to login and see what data we can get from it 
```
mysql -u <username> -p -h 127.0.0.1
```

```
mysql -u admin -p -h 127.0.0.1
```

I was using the wrong ip and this is the ip address that we have to use 
```
mysql -h 192.168.100.1 -u admin -p
```

```
!123SecureAdminDashboard321!
```


![[Pasted image 20240214212640.png]]

