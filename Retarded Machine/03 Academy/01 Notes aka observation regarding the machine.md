Will set the host on the file
┌──(root㉿kali)-[~/htb/academy]
└─# nano /etc/hosts
![[Pasted image 20230809044258.png]]

Default page
![[Pasted image 20230809044422.png]]

We get two options here login and register

Login.php
![[Pasted image 20230809044529.png]]

Register.php
![[Pasted image 20230809044501.png]]


![[Pasted image 20230809054441.png]]

How to get the PHP version that is running 
![[Pasted image 20230809072040.png]]

Will add the host name to /etc/hosts
When we add dev-staging-01.academy.htb/ 
we got this info from url http://dev-staging-01.academy.htb/ 
SERVER_ADMIN 	"admin@htb"
APP_KEY 	"base64:dBLUaMuZz7Iq06XtL/Xnz/90Ejq+DEEynggqubHWFj0="

