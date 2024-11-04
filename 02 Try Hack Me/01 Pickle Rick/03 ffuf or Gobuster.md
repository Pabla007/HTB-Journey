Directory : medium and common 
gobuster dir -u http://10.10.159.67 -x php -w /usr/share/wordlists/dirb/common.txt
![[Pasted image 20230905142109.png]]


Robots.txt
![[Pasted image 20230905142143.png]]



ffuf -request test.txt -request-proto http -w /usr/share/seclists/Passwords/xato-net-10-million-passwords-10000.txt:FUZZPASS -fs 200


A few examples of flags for the same are:

-mc : to specify Status code.
-ml: to specify amount of lines in response
-mr: to specify regex pattern
-ms: to specify response size
-mw: to specify amount of words in response