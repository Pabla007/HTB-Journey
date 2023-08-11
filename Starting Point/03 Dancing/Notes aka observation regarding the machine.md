- Here we have connected the machine with vpn using openvpn
- One the connection was established we run the ICMP echo request aka ping request to check if the machine is ruining or not.
		`ping <ip address> -c 4`
- Then run the Nmap scan
		 `nmap -T4 -p- -A <ip address>`
┌──(root㉿kali)-[~]
└─# nmap -T4 -Pn -A 10.129.1.12  
Starting Nmap 7.92 ( https://nmap.org ) at 2023-07-24 01:52 IST
Nmap scan report for 10.129.1.12
Host is up (0.39s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE       VERSION
135/tcp open  msrpc         Microsoft Windows RPC
139/tcp open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds?
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-07-23T12:07:50
|_  start_date: N/A
|_clock-skew: -8h15m34s

- Port 139/445 is for SMB (i.e. Server Message Block)

There 2 user and we download both the files (i.e. Worknotes and flag.txt)
