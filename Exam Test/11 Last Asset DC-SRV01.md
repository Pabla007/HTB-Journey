
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


So it's clear that one is refusing and one is not so the victim will be 10.201.11.30
But let's see how NTLM works as i didn't know how the algo works like i now we can only relay it but cannot replay it.

Now that we understand what an NTLM hash is and how it is hashed, we can look at how it responds and requests and why it can only be relayed and not replayed.

```

```

