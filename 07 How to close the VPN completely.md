```
# stop the service    
$ sudo /etc/init.d/openvpn stop

# find the process if it is still running for some reason
$ lsof -i | grep openvpn

# kill the proccess(s) by its PID
$ kill -9 <PID>

# if necessary restart the service again
$ sudo /etc/init.d/openvpn start
```