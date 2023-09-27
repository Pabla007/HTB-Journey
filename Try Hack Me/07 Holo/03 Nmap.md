Syntax: 
```
nmap -sV -sC -p- -v 10.200.95.0/24
```

- `sV` scans for service and version
- `sC` runs a script scan against open ports.
- `-p-` scans all ports 0 - 65535
- `-v` provides verbose output

Note for Aggresive scan's
Once you have identified open machines on the network and basic ports open, you can go back over the devices again individually with a more aggressive scan such as using the `-A` argument.

![[Pasted image 20230926224302.png]]

![[Pasted image 20230926224524.png]]
![[Pasted image 20230926224504.png]]

```
└─# nmap -T4 -p- -A 10.200.95.33        
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-26 13:13 EDT
Warning: 10.200.95.33 giving up on port because retransmission cap hit (6).
Nmap scan report for 10.200.95.33
Host is up (0.15s latency).
Not shown: 65510 closed tcp ports (reset)
PORT      STATE    SERVICE VERSION
22/tcp    open     ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 7f:16:f7:29:17:d6:4c:79:3c:06:37:b1:bd:9f:00:09 (RSA)
|   256 a0:5b:52:c5:60:2c:83:a5:c7:d0:ac:50:99:0a:f8:5e (ECDSA)
|_  256 22:f5:fd:70:ff:53:bf:9f:8b:b3:e6:a0:fb:34:0c:b0 (ED25519)
80/tcp    open     http    Apache httpd 2.4.29 ((Ubuntu))
|_http-generator: WordPress 5.5.3
|_http-title: holo.live
| http-robots.txt: 21 disallowed entries (15 shown)
| /var/www/wordpress/index.php 
| /var/www/wordpress/readme.html /var/www/wordpress/wp-activate.php 
| /var/www/wordpress/wp-blog-header.php /var/www/wordpress/wp-config.php 
| /var/www/wordpress/wp-content /var/www/wordpress/wp-includes 
| /var/www/wordpress/wp-load.php /var/www/wordpress/wp-mail.php 
| /var/www/wordpress/wp-signup.php /var/www/wordpress/xmlrpc.php 
| /var/www/wordpress/license.txt /var/www/wordpress/upgrade 
|_/var/www/wordpress/wp-admin /var/www/wordpress/wp-comments-post.php
|_http-server-header: Apache/2.4.29 (Ubuntu)
10923/tcp filtered unknown
15396/tcp filtered unknown
19829/tcp filtered unknown
22605/tcp filtered unknown
25245/tcp filtered unknown
25357/tcp filtered unknown
26135/tcp filtered unknown
27885/tcp filtered unknown
29242/tcp filtered unknown
29408/tcp filtered unknown
30777/tcp filtered unknown
32308/tcp filtered unknown
33060/tcp open     mysqlx?
| fingerprint-strings: 
|   DNSStatusRequestTCP, LDAPSearchReq, NotesRPC, SSLSessionReq, TLSSessionReq, X11Probe, afp: 
|     Invalid message"
|_    HY000
36457/tcp filtered unknown
38700/tcp filtered unknown
40208/tcp filtered unknown
43053/tcp filtered unknown
45575/tcp filtered unknown
49285/tcp filtered unknown
49361/tcp filtered unknown
49545/tcp filtered unknown
60213/tcp filtered unknown
64902/tcp filtered unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port33060-TCP:V=7.94%I=7%D=9/26%Time=651313DA%P=x86_64-pc-linux-gnu%r(N

```

```
nmap -sS -T4 -p- -A 10.200.95.33  


Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-26 13:17 EDT
Nmap scan report for 10.200.95.33
Host is up (0.15s latency).
Not shown: 65532 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 7f:16:f7:29:17:d6:4c:79:3c:06:37:b1:bd:9f:00:09 (RSA)
|   256 a0:5b:52:c5:60:2c:83:a5:c7:d0:ac:50:99:0a:f8:5e (ECDSA)
|_  256 22:f5:fd:70:ff:53:bf:9f:8b:b3:e6:a0:fb:34:0c:b0 (ED25519)
80/tcp    open  http    Apache httpd 2.4.29 ((Ubuntu))
| http-robots.txt: 21 disallowed entries (15 shown)
| /var/www/wordpress/index.php 
| /var/www/wordpress/readme.html /var/www/wordpress/wp-activate.php 
| /var/www/wordpress/wp-blog-header.php /var/www/wordpress/wp-config.php 
| /var/www/wordpress/wp-content /var/www/wordpress/wp-includes 
| /var/www/wordpress/wp-load.php /var/www/wordpress/wp-mail.php 
| /var/www/wordpress/wp-signup.php /var/www/wordpress/xmlrpc.php 
| /var/www/wordpress/license.txt /var/www/wordpress/upgrade 
|_/var/www/wordpress/wp-admin /var/www/wordpress/wp-comments-post.php
|_http-generator: WordPress 5.5.3
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: holo.live
33060/tcp open  mysqlx?
| fingerprint-strings: 
|   DNSStatusRequestTCP, LDAPSearchReq, NotesRPC, SSLSessionReq, TLSSessionReq, X11Probe, afp: 
|     Invalid message"
|_    HY000
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port33060-TCP:V=7.94%I=7%D=9/26%Time=651315AF%P=x86_64-pc-linux-gnu%r(N

```

