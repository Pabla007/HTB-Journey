
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

