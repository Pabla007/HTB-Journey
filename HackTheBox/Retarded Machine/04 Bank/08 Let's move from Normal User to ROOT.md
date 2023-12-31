See how they have done Excryption
Now Encryption is the Rabbit hole as we don't know how it's happening that why most people didn't liked this box. And that's the DEAD end for this
![[Pasted image 20230819113949.png]]


When we cat the bankreports.txt we got the user id of  Chris but we already got that through enumeration without the help of the shell.

But when we enumerate in the inc folder and cat that we found the root id and password
![[Pasted image 20230819114327.png]]

User id and password for MySql
root 
!@#S3cur3P4ssw0rd!@#

![[Pasted image 20230819114803.png]]
Get a shell in sql
\! /bin/sh

But we didn't got lucky and escalated to Root privileges.

Let's try the SSH with root and chris password
![[Pasted image 20230819115413.png]]

we were not able to make any connection there as well.

**Now let's run the enumeration scripts**
Will host the script from our directory 
┌──(kali㉿kali)-[/opt/linpeas]
└─$ python3 -m http.server 8080 -b 10.10.16.7    
Serving HTTP on 10.10.16.7 port 8080 (http://10.10.16.7:8080/) ...
![[Pasted image 20230819121846.png]]
Let's try writing the passwd file
![[Pasted image 20230819122812.png]]
As we have edited the passwd file let's try to ssh and see what happens

![[Pasted image 20230819122946.png]]
5eb414d40af804d2fda5d7f0e61773ca


![[Pasted image 20230819122006.png]]
/var/htb/emergency
/var/htb/bin/emergency
Will run this and see if we become Root user or not

Hahah we got the root shell 
![[Pasted image 20230819122228.png]]


We got the user key in the chris folder
![[Pasted image 20230819121105.png]]

1c31836b9c5b64b4cf764f499ffdc07f 


1c31836b9c5b64b4cf764f499ffdc07f
# cat user.txt
1c31836b9c5b64b4cf764f499ffdc07f

openssl passwd --help

5eb414d40af804d2fda5d7f0e61773ca

sed -n 'l' root.txt
5eb414d40af804d2fda5d7f0e61773ca$
