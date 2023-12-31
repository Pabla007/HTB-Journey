We have to Use the SYN scan in order to get the 3rd port which was missing
![[Pasted image 20230814095241.png]]
┌──(root㉿kali)-[~/htb/bank]
└─# nmap -sS -T4 -A 10.10.10.29 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-14 00:20 EDT
Nmap scan report for bank.htb (10.10.10.29)
Host is up (0.33s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 08:ee:d0:30:d5:45:e4:59:db:4d:54:a8:dc:5c:ef:15 (DSA)
|   2048 b8:e0:15:48:2d:0d:f0:f1:73:33:b7:81:64:08:4a:91 (RSA)
|   256 a0:4c:94:d1:7b:6e:a8:fd:07:fe:11:eb:88:d5:16:65 (ECDSA)
|_  256 2d:79:44:30:c8:bb:5e:8f:07:cf:5b:72:ef:a1:6d:67 (ED25519)
53/tcp open  domain  ISC BIND 9.9.5-3ubuntu0.14 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.9.5-3ubuntu0.14-Ubuntu
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
| http-title: HTB Bank - Login
|_Requested resource was login.php
|_http-server-header: Apache/2.4.7 (Ubuntu)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94%E=4%D=8/14%OT=22%CT=1%CU=40541%PV=Y%DS=2%DC=T%G=Y%TM=64D9ABB
OS:7%P=x86_64-pc-linux-gnu)SEQ(SP=103%GCD=1%ISR=10C%TI=Z%CI=I%II=I%TS=8)SEQ
OS:(SP=104%GCD=1%ISR=10D%TI=Z%II=I%TS=8)SEQ(SP=104%GCD=1%ISR=10D%TI=Z%CI=I%
OS:II=I%TS=8)OPS(O1=M53AST11NW7%O2=M53AST11NW7%O3=M53ANNT11NW7%O4=M53AST11N
OS:W7%O5=M53AST11NW7%O6=M53AST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=712
OS:0%W6=7120)ECN(R=Y%DF=Y%T=40%W=7210%O=M53ANNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40
OS:%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=
OS:%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%
OS:W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=
OS:)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%
OS:DFI=N%T=40%CD=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 1723/tcp)
HOP RTT       ADDRESS
1   358.93 ms 10.10.16.1
2   159.74 ms bank.htb (10.10.10.29)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 45.35 seconds
                                                                                                                                                             
┌──(root㉿kali)-[~/htb/bank]
└─# 


![[Pasted image 20230813133431.png]]

┌──(root㉿kali)-[~/htb/bank]
└─# nmap -T4 -Pn -A 10.10.10.29 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-13 03:50 EDT
Nmap scan report for 10.10.10.29
Host is up (0.34s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE    VERSION
22/tcp open  tcpwrapped
|_ssh-hostkey: ERROR: Script execution failed (use -d to debug)
53/tcp open  domain     ISC BIND 9.9.5-3ubuntu0.14 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.9.5-3ubuntu0.14-Ubuntu
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94%E=4%D=8/13%OT=53%CT=1%CU=34946%PV=Y%DS=2%DC=T%G=Y%TM=64D88B8
OS:C%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=10F%TI=Z%II=I%TS=8)SEQ(SP=1
OS:06%GCD=1%ISR=10F%TI=Z%CI=I%II=I%TS=8)OPS(O1=M53AST11NW7%O2=M53AST11NW7%O
OS:3=M53ANNT11NW7%O4=M53AST11NW7%O5=M53AST11NW7%O6=M53AST11)WIN(W1=7120%W2=
OS:7120%W3=7120%W4=7120%W5=7120%W6=7120)ECN(R=Y%DF=Y%T=40%W=7210%O=M53ANNSN
OS:W7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%D
OS:F=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O
OS:=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%R
OS:IPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   410.87 ms 10.10.16.1
2   215.60 ms 10.10.10.29

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 45.70 seconds


![[Pasted image 20230813130327.png]]

┌──(root㉿kali)-[~/htb/bank]
└─# nmap -sF -v -v -Pn 10.10.10.29      
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-13 03:31 EDT
Initiating Parallel DNS resolution of 1 host. at 03:31
Completed Parallel DNS resolution of 1 host. at 03:31, 0.01s elapsed
Initiating FIN Scan at 03:31
Scanning 10.10.10.29 [1000 ports]
Completed FIN Scan at 03:32, 32.73s elapsed (1000 total ports)
Nmap scan report for 10.10.10.29
Host is up, received user-set (0.51s latency).
Scanned at 2023-08-13 03:31:53 EDT for 33s
Not shown: 998 closed tcp ports (reset)
PORT   STATE         SERVICE REASON
22/tcp open|filtered ssh     no-response
53/tcp open|filtered domain  no-response

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 32.81 seconds
           Raw packets sent: 1080 (43.200KB) | Rcvd: 1072 (42.880KB)
