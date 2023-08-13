

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
