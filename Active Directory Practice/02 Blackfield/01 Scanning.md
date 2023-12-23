
```
 nmap -sS -T4 -p- 10.10.10.192           
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-17 00:19 EST
Nmap scan report for 10.10.10.192
Host is up (0.27s latency).
Not shown: 65527 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
389/tcp  open  ldap
445/tcp  open  microsoft-ds
593/tcp  open  http-rpc-epmap
3268/tcp open  globalcatLDAP
5985/tcp open  wsman

Nmap done: 1 IP address (1 host up) scanned in 448.53 seconds
```


```
nmap -T4 -p- -A 10.10.10.192            
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-17 00:19 EST
Nmap scan report for 10.10.10.192
Host is up (0.40s latency).
Not shown: 65526 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-11-17 12:28:17Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  tcpwrapped
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local0., Site: Default-First-Site-Name)
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2019 (86%)
Aggressive OS guesses: Microsoft Windows Server 2019 (86%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: 7h00m00s
| smb2-time: 
|   date: 2023-11-17T12:29:05
|_  start_date: N/A

TRACEROUTE (using port 135/tcp)
HOP RTT       ADDRESS
1   477.57 ms 10.10.16.1
2   477.79 ms 10.10.10.192

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 639.42 seconds
```
