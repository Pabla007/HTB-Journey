
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