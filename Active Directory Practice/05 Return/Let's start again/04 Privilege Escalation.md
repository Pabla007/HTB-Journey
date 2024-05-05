
```
ldapdomaindump ldaps://10.10.11.108 -u 'RETURN\svc-printer' -p '1edFg43012!!'
```
![[Pasted image 20240505194413.png]]


```
bloodhound-python -d RETURN.local -u svc-printer -p '1edFg43012!!' -ns 10.10.11.108 -c all
```
![[Pasted image 20240505194335.png]]


```

```