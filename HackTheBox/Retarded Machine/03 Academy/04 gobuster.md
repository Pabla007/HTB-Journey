┌──(root㉿kali)-[~/htb/academy]
└─# gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://academy.htb -o gobuster/vhost-sub.txt


┌──(root㉿kali)-[~/htb/academy]
└─# gobuster dir -u http://academy.htb -x php -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt -o gobuster/dir-root.log 

![[Pasted image 20230809064201.png]]

I simply made a user with with roleid=1
user=admin
passwd= 123456
![[Pasted image 20230809065507.png]]

When we go to adim.php was able to login using the above credentials and got this output








