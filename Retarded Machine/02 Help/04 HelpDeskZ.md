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



On occasions you get reverse shell but not tty shell, you can get it via the command-  
_python -c ‘import pty; pty.spawn(“/bin/bash”)’_  
  
Upgrading to fully interactive TTY shell (working arrow keys and CTRL-C won’t kill the reverse shell session). After python -c ‘import pty; pty.spawn(“/bin/bash”)’ , hit CTRL-z (this will background the nc session). then on kali machine type “stty raw -echo “ and enter. again, type “fg” and enter. (input cannot be seen after hitting stty command so simply type fg and enter).  
_This will now give fully interactive TTY shell as if you were logged in via SSH._