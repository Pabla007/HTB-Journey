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
![[Pasted image 20230809065711.png]]

Balance-transfer was the directory that we were looking but was not able to find using 
ffuf or gobuster along with the wordlists that we had provided.

![[Pasted image 20230814114132.png]]

we have to find the file that is not encrypted for that we have to wget the folder and run Burpsuite on it
But if we scan the size and found this one file
http://bank.htb/balance-transfer/68576f20e9732f1b2edc4df5b8533230.acc
![[Pasted image 20230814114933.png]]

--ERR ENCRYPT FAILED
+=================+
| HTB Bank Report |
+=================+

===UserAccount===
Full Name: Christos Christopoulos
Email: chris@bank.htb
Password: !##HTBB4nkP4ssw0rd!##
CreditCards: 5
Transactions: 39
Balance: 8842803 .
===UserAccount===
