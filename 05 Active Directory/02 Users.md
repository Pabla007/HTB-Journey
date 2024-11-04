
```
Copy from: Administrator

Full name: Tony Stark

User logon name: tstark@MARVEL.local

The password never expires.

password12345!
```

```
Copy from: Administrator

Full name: SQL Service

User logon name: SQLService@MARVEL.local

The password never expires.

MYpassword123#
```

```
Full name: Frank Castle

User logon name: fcastle@MARVEL.local

The password never expires.

Password1
```

```
Full name: Peter Parker

User logon name: pparker@MARVEL.local

The password never expires.

Password2
```

```
hackme
C:\Shares\hackme
\\HYDRA-DC\hackme
```

```
setspn -a HYDRA-DC/SQLService.MARVEL.local:6011 MARVEL\SQLService
```
![[Pasted image 20231216144002.png]]

```
setspn -T MARVEL.local -Q */*
```
![[Pasted image 20231216144104.png]]

```
IPv4 Address. . . . . . . . . . . : 192.168.17.139
```
Will set a static IP address


Ram Management 
Kali Linus : 2GB
Windows Server : 2 GB
Punisher : 4 GB
Spiderman : 2GB

Change the DNS server of the machines [i.e. Punisher and Spiderman]

```
Marvel.local
```

```
administrator
P@$$w0rd!
```

![[Pasted image 20231216153658.png]]

We are able to join the computer with the domain.
```
Password1!
```
![[Pasted image 20231216154258.png]]

To login in locally
```
.\peterparker
Password1
```


So now we are able to login in locally and setup the account
![[Pasted image 20231216160030.png]]
And mapped the network drive successfully.

The setup of the lab is over and will do the necessary tweaks with time.