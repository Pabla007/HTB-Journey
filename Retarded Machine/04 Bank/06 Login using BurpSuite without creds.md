http://10.10.10.29/
![[Pasted image 20230819083056.png]]
As we know we were getting the default page in this scenario

So let's intercept the request and see what's happening:
![[Pasted image 20230819083156.png]]
We get the 200 ok request but will see if try to change the host address and see what we get
bank.htb
![[Pasted image 20230819083302.png]]
We can see something is being found here
![[Pasted image 20230819083340.png]]


It's not vulnerable to SQL injection. 
And will turn on the server intercepts  as the option has changed follow this ss
![[Pasted image 20230819102557.png]]

We can automatically rewrite all the responses 
![[Pasted image 20230819103023.png]]

When we turn the intercept on and off we can see the page is not redirected to login page
http://bank.htb/index.php
![[Pasted image 20230819103613.png]]

http://bank.htb/support.php
![[Pasted image 20230819103631.png]]

Disable the re-write cuz we don't want to it anymore.
