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

