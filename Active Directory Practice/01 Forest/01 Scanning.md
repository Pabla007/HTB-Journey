
```
nmap -T4 -p- forest.htb 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-09 08:20 EST
Warning: 10.10.10.161 giving up on port because retransmission cap hit (6).
Nmap scan report for forest.htb (10.10.10.161)
Host is up (0.52s latency).
Not shown: 65511 closed tcp ports (reset)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49671/tcp open  unknown
49676/tcp open  unknown
49677/tcp open  unknown
49684/tcp open  unknown
49703/tcp open  unknown
49939/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 2052.61 seconds
```

```
 nmap -T4 -p- -A forest.htb
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-09 08:21 EST
Warning: 10.10.10.161 giving up on port because retransmission cap hit (6).
Nmap scan report for forest.htb (10.10.10.161)
Host is up (0.65s latency).
Not shown: 65511 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec?
135/tcp   open  msrpc?
139/tcp   open  netbios-ssn?
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
445/tcp   open  ��+V        Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  adws?
47001/tcp open  winrm?
| fingerprint-strings: 
|   JavaRMI: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/html; charset=us-ascii
|     Server: Microsoft-HTTPAPI/2.0
|     Date: Thu, 09 Nov 2023 14:02:38 GMT
|     Connection: close
|     Content-Length: 326
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd">
|     <HTML><HEAD><TITLE>Bad Request</TITLE>
|     <META HTTP-EQUIV="Content-Type" Content="text/html; charset=us-ascii"></HEAD>
|     <BODY><h2>Bad Request - Invalid Verb</h2>
|     <hr><p>HTTP Error 400. The request verb is invalid.</p>
|_    </BODY></HTML>
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49676/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49677/tcp open  msrpc         Microsoft Windows RPC
49684/tcp open  unknown
49703/tcp open  unknown
49939/tcp open  unknown
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port139-TCP:V=7.94%I=7%D=11/9%Time=654CE4E2%P=x86_64-pc-linux-gnu%r(Get
SF:Request,5,"\x83\0\0\x01\x8f");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port47001-TCP:V=7.94%I=7%D=11/9%Time=654CE4E2%P=x86_64-pc-linux-gnu%r(J
SF:avaRMI,1F9,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text
SF:/html;\x20charset=us-ascii\r\nServer:\x20Microsoft-HTTPAPI/2\.0\r\nDate
SF::\x20Thu,\x2009\x20Nov\x202023\x2014:02:38\x20GMT\r\nConnection:\x20clo
SF:se\r\nContent-Length:\x20326\r\n\r\n<!DOCTYPE\x20HTML\x20PUBLIC\x20\"-/
SF:/W3C//DTD\x20HTML\x204\.01//EN\"\"http://www\.w3\.org/TR/html4/strict\.
SF:dtd\">\r\n<HTML><HEAD><TITLE>Bad\x20Request</TITLE>\r\n<META\x20HTTP-EQ
SF:UIV=\"Content-Type\"\x20Content=\"text/html;\x20charset=us-ascii\"></HE
SF:AD>\r\n<BODY><h2>Bad\x20Request\x20-\x20Invalid\x20Verb</h2>\r\n<hr><p>
SF:HTTP\x20Error\x20400\.\x20The\x20request\x20verb\x20is\x20invalid\.</p>
SF:\r\n</BODY></HTML>\r\n");
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94%E=4%D=11/9%OT=53%CT=1%CU=36142%PV=Y%DS=2%DC=T%G=Y%TM=654CE5C
OS:6%P=x86_64-pc-linux-gnu)SEQ(SP=100%GCD=1%ISR=10B%TI=I%CI=I%II=I%TS=A)SEQ
OS:(SP=100%GCD=1%ISR=10B%TI=RD%CI=I%II=I%TS=A)SEQ(SP=100%GCD=1%ISR=10B%TI=R
OS:D%CI=RD%II=I%TS=9)OPS(O1=M53ANW8ST11%O2=M53ANW8ST11%O3=M53ANW8NNT11%O4=M
OS:53ANW8ST11%O5=M53ANW8ST11%O6=M53AST11)WIN(W1=2000%W2=2000%W3=2000%W4=200
OS:0%W5=2000%W6=2000)ECN(R=Y%DF=Y%T=80%W=2000%O=M53ANW8NNS%CC=Y%Q=)T1(R=Y%D
OS:F=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD=0
OS:%Q=)T3(R=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=80%W=0%S=
OS:A%A=O%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=
OS:Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=A
OS:R%O=%RD=0%Q=)U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%R
OS:UD=G)IE(R=Y%DFI=N%T=80%CD=Z)

Network Distance: 2 hops
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST
|   NetBIOS computer name: FOREST\x00
|   Domain name: htb.local
|   Forest name: htb.local
|   FQDN: FOREST.htb.local
|_  System time: 2023-11-09T06:04:10-08:00
| smb2-time: 
|   date: 2023-11-09T14:04:11
|_  start_date: 2023-11-09T13:00:30
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
|_clock-skew: mean: 2h46m53s, deviation: 4h37m11s, median: 6m51s

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   566.15 ms 10.10.16.1
2   895.52 ms forest.htb (10.10.10.161)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2311.28 seconds

```