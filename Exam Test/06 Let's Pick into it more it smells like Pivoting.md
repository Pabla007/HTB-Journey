
So i guess we should have persistent access 
```
L-SRV01
10.201.11.33

L-SRV02
192.168.100.100

DC-SRV01
10.201.11.33
```

Username and Password
```
linux-admin
```

```
linuxrulez
```

Let's try ssh fingers crossed to get the 
```
ssh linux-admin@10.201.11.33
```

And we are in so we don't have the problem of getting rev-shell again and again


So i was not able to get how to find the pivoting but let's give it a try for myself what i have learnt and how can i configure and carry out the attack.


```
./nmap -sn -n 10.201.11.0/24 -oA Ping-Sweep

Starting Nmap 6.49BETA1 ( http://nmap.org ) at 2024-08-22 13:54 UTC
Cannot find nmap-payloads. UDP payloads are disabled.
Nmap scan report for 10.201.11.30
Host is up (0.00087s latency).
Nmap scan report for 10.201.11.31
Host is up (0.0020s latency).
Nmap scan report for 10.201.11.33
Host is up (0.00014s latency).
Nmap scan report for 10.201.11.35
Host is up (0.0011s latency).
Nmap scan report for 10.201.11.250
Host is up (0.0017s latency).
Nmap done: 256 IP addresses (5 hosts up) scanned in 5.01 seconds
```


## So we have 5 hosts lets check  30/31/33/35


I think got my hands on the the Domain controller (i.e. 10.201.11.30)
## 10.201.11.30 | DC-SRV01
```
nmap -T4 -p- -A -Pn 10.201.11.30
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 13:59 UTC
Nmap scan report for ip-10-201-11-30.eu-west-1.compute.internal (10.201.11.30)
Host is up (0.0015s latency).
Not shown: 65509 closed ports
PORT      STATE SERVICE       VERSION
53/tcp    open  domain?
| fingerprint-strings: 
|   DNSVersionBindReqTCP: 
|     version
|_    bind
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2024-08-22 14:01:44Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: holo.live0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: holo.live0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: HOLOLIVE
|   NetBIOS_Domain_Name: HOLOLIVE
|   NetBIOS_Computer_Name: DC-SRV01
|   DNS_Domain_Name: holo.live
|   DNS_Computer_Name: DC-SRV01.holo.live
|   DNS_Tree_Name: holo.live
|   Product_Version: 10.0.17763
|_  System_Time: 2024-08-22T14:04:00+00:00
| ssl-cert: Subject: commonName=DC-SRV01.holo.live
| Not valid before: 2024-08-19T18:15:57
|_Not valid after:  2025-02-18T18:15:57
|_ssl-date: 2024-08-22T14:04:14+00:00; 0s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49677/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49678/tcp open  msrpc         Microsoft Windows RPC
49683/tcp open  msrpc         Microsoft Windows RPC
49694/tcp open  msrpc         Microsoft Windows RPC
49708/tcp open  msrpc         Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-TCP:V=7.80%I=7%D=8/22%Time=66C744CD%P=x86_64-pc-linux-gnu%r(DNSV
SF:ersionBindReqTCP,20,"\0\x1e\0\x06\x81\x04\0\x01\0\0\0\0\0\0\x07version\
SF:x04bind\0\0\x10\0\x03");
Service Info: Host: DC-SRV01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_nbstat: NetBIOS name: DC-SRV01, NetBIOS user: <unknown>, NetBIOS MAC: 02:22:a7:11:71:01 (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2024-08-22T14:04:00
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 286.12 seconds
```

## 10.201.11.31 |  S-SRV01
```
nmap -T4 -p- -A -Pn 10.201.11.31
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 14:10 UTC
Nmap scan report for ip-10-201-11-31.eu-west-1.compute.internal (10.201.11.31)
Host is up (0.00090s latency).
Not shown: 65517 closed ports
PORT      STATE SERVICE       VERSION
22/tcp    open  ssh           OpenSSH for_Windows_7.7 (protocol 2.0)
| ssh-hostkey: 
|   2048 7c:c4:6b:4c:f5:73:58:dc:d6:ac:3c:bd:21:7e:67:3b (RSA)
|   256 f1:83:ba:c1:94:ab:35:7c:44:00:26:55:9d:13:7b:94 (ECDSA)
|_  256 32:86:c6:52:b3:61:27:71:ff:6d:9f:8d:f9:86:16:83 (ED25519)
80/tcp    open  http          Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.4.11)
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.4.11
|_http-title: Holo.live - Virtual Events
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.4.11)
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.4.11
|_http-title: Holo.live - Virtual Events
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
445/tcp   open  microsoft-ds?
3306/tcp  open  mysql?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: HOLOLIVE
|   NetBIOS_Domain_Name: HOLOLIVE
|   NetBIOS_Computer_Name: S-SRV01
|   DNS_Domain_Name: holo.live
|   DNS_Computer_Name: S-SRV01.holo.live
|   DNS_Tree_Name: holo.live
|   Product_Version: 10.0.17763
|_  System_Time: 2024-08-22T14:14:52+00:00
| ssl-cert: Subject: commonName=S-SRV01.holo.live
| Not valid before: 2024-08-19T18:16:11
|_Not valid after:  2025-02-18T18:16:11
|_ssl-date: 2024-08-22T14:15:05+00:00; 0s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49672/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_nbstat: NetBIOS name: S-SRV01, NetBIOS user: <unknown>, NetBIOS MAC: 02:aa:10:45:62:fb (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2024-08-22T14:14:52
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 292.95 seconds
```

## 10.201.11.35   PC-FILESRV01
```
nmap -T4 -p- -A -Pn 10.201.11.35
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 14:17 UTC
Nmap scan report for ip-10-201-11-35.eu-west-1.compute.internal (10.201.11.35)
Host is up (0.00059s latency).
Not shown: 65520 closed ports
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: HOLOLIVE
|   NetBIOS_Domain_Name: HOLOLIVE
|   NetBIOS_Computer_Name: PC-FILESRV01
|   DNS_Domain_Name: holo.live
|   DNS_Computer_Name: PC-FILESRV01.holo.live
|   DNS_Tree_Name: holo.live
|   Product_Version: 10.0.17763
|_  System_Time: 2024-08-22T14:20:40+00:00
| ssl-cert: Subject: commonName=PC-FILESRV01.holo.live
| Not valid before: 2024-08-19T18:16:12
|_Not valid after:  2025-02-18T18:16:12
|_ssl-date: 2024-08-22T14:20:45+00:00; 0s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49672/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_nbstat: NetBIOS name: PC-FILESRV01, NetBIOS user: <unknown>, NetBIOS MAC: 02:30:42:3c:d0:9b (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2024-08-22T14:20:40
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 180.55 seconds
```


```
nmap -T4 -p- -A -Pn 10.201.11.250
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 14:26 UTC
Nmap scan report for ip-10-201-11-250.eu-west-1.compute.internal (10.201.11.250)
Host is up (0.012s latency).
Not shown: 65533 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 27:fc:e4:b2:7d:71:8a:ed:86:4b:b6:9f:67:41:8f:c0 (RSA)
|   256 73:21:11:d0:4f:9b:48:9f:10:97:bc:76:d2:a0:3d:1f (ECDSA)
|_  256 59:78:b9:63:02:27:dd:22:d8:81:5a:48:7d:7e:95:d4 (ED25519)
1337/tcp open  http    Node.js Express framework
|_http-title: Error
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.24 seconds
```

