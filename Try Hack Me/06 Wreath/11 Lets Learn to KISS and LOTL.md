
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

