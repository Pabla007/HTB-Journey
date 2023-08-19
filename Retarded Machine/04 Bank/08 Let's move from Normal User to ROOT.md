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
