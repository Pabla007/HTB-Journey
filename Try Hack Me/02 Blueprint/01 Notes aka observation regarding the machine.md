Error while we try to connect to the IP addrees
![[Pasted image 20230906214949.png]]

But when we connect with port 8080 we got something
![[Pasted image 20230906215018.png]]



I think we should target 
SMB port 139 cuz that looks juicy according to me.

So my Hunch was wrong as it's not vulnerable to MS170-01 aka etherblue let's see for RPC
![[Pasted image 20230906214810.png]]

As we have checked everything now something seems suspicious of this broken website
![[Pasted image 20230906232336.png]]

![[Pasted image 20230906232317.png]]

So let's check it out as well.
Here i have simply copied the code using -m 
root㉿kali)-[~/TryHackMe/BluePrint]
└─# searchsploit -m php/webapps/44374.py
![[Pasted image 20230906232935.png]]

