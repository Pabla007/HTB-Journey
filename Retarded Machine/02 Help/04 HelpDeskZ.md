Will not install the the program but will enumerate the directory structure from the github
https://github.com/ViktorNova/HelpDeskZ/tree/master/uploads/tickets

and got to know the upload file location.

As the attack didn't worked and when we see the code in the depth we will be able to notice check the box time using burpsuite for that will start the intercept on.

![[Pasted image 20230803021607.png]]

Options we will turn the server response on
![[Pasted image 20230803021728.png]]

Than will forward the request and will get the response and the time we needed.
![[Pasted image 20230803021821.png]]

Our system time
![[Pasted image 20230803021911.png]]

So as we can see the server is running behind and the timezone is different so we are facing a problem due to that.

We have used the requests and able to retrive the date from the htb server head and will convert it using a tool called https://strftime.org/

![[Pasted image 20230803024755.png]]
Python output : 1691011012

We got epoch to time https://www.epochconverter.com/
![[Pasted image 20230803024936.png]]

I manually convert the md5 and passed in the url
![[Pasted image 20230811214327.png]]
Simply pass the url in the web-browser
http://help.htb/support/uploads/tickets/897cb9bb1135c3173b1c829a6584433c.php
http://10.10.10.121/support/uploads/tickets/897cb9bb1135c3173b1c829a6584433c.php

Finally got the shell
![[Pasted image 20230811213819.png]]

![[Pasted image 20230811214114.png]]

$ cat user.txt
ead45582d912deb29028b1f3c21bd05c

When we use 
Command: ls -la
![[Pasted image 20230811215035.png]]

What is the kernel name running on the Helpdeskz
![[Pasted image 20230811215735.png]]
`uname -a` will give the required information.
Linux help 4.4.0-116-generic  `#140-Ubuntu` SMP Mon Feb 12 21:23:04 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
