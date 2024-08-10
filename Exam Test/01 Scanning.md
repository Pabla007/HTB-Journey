
```
nmap -sS 10.201.11.0-255/24 -oA ping-sweep 
```

```
└─# nmap -sS 10.201.11.0-255/24 -oA ping-sweep 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-09 02:42 IST
Nmap scan report for 10.201.11.33
Host is up (0.14s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap scan report for 10.201.11.250
Host is up (0.14s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 256 IP addresses (2 hosts up) scanned in 38.45 seconds
```

1st step 1st 
Will do the scanning of the last octant (i.e. 0-255) and got to know that we got 2 live hosts.
```
10.201.11.33
```

```
10.201.11.250
```


2nd Step is that we will scan both the Ip's to see which services are running on them.
```
nmap -sS 10.201.11.33 10.201.145.250 -v -oA Initial-Scan-Subnet1-Hosts
```


