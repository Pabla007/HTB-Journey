
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
\\10.201.11.31
```

