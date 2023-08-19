I have the ffuf as gobuster was not installed as of now

ffuf -w /usr/share/wordlists/dirb/common.txt:FUZZ -u http://bank.htb//FUZZ
![[Pasted image 20230814101936.png]]
http://bank.htb/inc/
![[Pasted image 20230814101433.png]]
header.php was not found
rest footer,ticket,user was empty but page was loading

Forbidden 
http://bank.htb/server-status
http://bank.htb/uploads/

![[Pasted image 20230814101421.png]]

dirbuster
![[Pasted image 20230814210031.png]]
![[Pasted image 20230814205958.png]]
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

This is the page that we can see after we login 
![[Pasted image 20230819081623.png]]

Now we have to check different things in support like upload vulnerability or SQL injection.
![[Pasted image 20230819081716.png]]

