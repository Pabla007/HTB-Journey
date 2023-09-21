- Here we have connected the machine with vpn using openvpn
- One the connection was established we run the ICMP echo request aka ping request to check if the machine is ruining or not.
		`ping <ip address> -c 4`
- Then run the Nmap scan
		 `nmap -T4 -p- -A <ip address>`
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt

Network Distance: 2 hops
Service Info: OS: Unix

- Port 21 is for FTP (i.e. File Transfer Protocol)
- What acronym is used for the secure version of FTP? 
		`SFTP (Secure File Transfer Protocol)`

- What is username that is used over FTP when you want to log in without having an account?
		`anonymous`
		
![[Pasted image 20230722130210.png]]

┌──(root㉿kali)-[~]
└─# cat flag.txt  
035db21c881520061c53e0536e44f815  