
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


## Host File
```
127.0.0.1       localhost
127.0.1.1       kali
10.10.63.33    vulnversity.thm
10.10.222.82  cmess.thm
10.10.222.82  dev.cmess.thm
10.10.224.185  ultratech.thm:31331
10.10.224.185  ultratech.thm:8081

#Hacking
10.10.30.47  lazyadmin.thm
10.10.39.13  anonymous.thm
10.10.246.4 tomghost.thm
10.10.38.151 convertmyvideo.thm
10.10.37.57 blaster.thm

#HackTheBox
10.10.10.5 devel.htb
10.10.10.74 chatterbox.htb
10.10.10.97 secnotes.htb
10.10.10.63 jeeves.htb
10.10.10.98 access.htb
10.10.10.11 arctic.htb
10.10.10.9  bastard.htb
10.10.10.134 bastian.htb
10.10.10.125 querier.htb
10.10.11.174 support.htb

#Active Directory
10.10.10.161 forest.htb htb.local forest
10.10.10.192 blackfield.htb backfield.local BLACKFIELD.local0 DC01.BLACKFIELD.LOCAL

#Holo
10.200.107.33    holo.live
10.200.107.33    www.holo.live
10.200.107.33    admin.holo.live
10.200.107.33    dev.holo.live

::1             localhost ip6-localhost ip6-loopback
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters
```

