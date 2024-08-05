
Got a reverse shell with full access to have to write some code dumb shell to full aceess shell

```
python3 -c "__import__('pty').spawn('/bin/bash')"
stty -raw echo;fg 
reset.

export TERM=xterm

```


