Let's run the Nmap scan
```
cat nmap_sS.txt.nmap 
# Nmap 7.94 scan initiated Wed Dec  6 00:03:42 2023 as: nmap -sS -T4 -p 1-15000 -oA nmap_sS.txt 10.200.85.200
Nmap scan report for 10.200.85.200
Host is up (0.16s latency).
Not shown: 14956 filtered tcp ports (no-response), 39 filtered tcp ports (admin-prohibited)
PORT      STATE  SERVICE
22/tcp    open   ssh
80/tcp    open   http
443/tcp   open   https
9090/tcp  closed zeus-admin
10000/tcp open   snet-sensor-mgmt

# Nmap done at Wed Dec  6 00:04:58 2023 -- 1 IP address (1 host up) scanned in 75.88 seconds
```

```
cat nmap.txt.nmap                 
# Nmap 7.94 scan initiated Wed Dec  6 00:03:34 2023 as: nmap -T4 -p 1-15000 -A -oA nmap.txt 10.200.85.200
Nmap scan report for 10.200.85.200
Host is up (0.16s latency).
Not shown: 14953 filtered tcp ports (no-response), 42 filtered tcp ports (admin-prohibited)
PORT      STATE  SERVICE    VERSION
22/tcp    open   ssh        OpenSSH 8.0 (protocol 2.0)
| ssh-hostkey: 
|   3072 9c:1b:d4:b4:05:4d:88:99:ce:09:1f:c1:15:6a:d4:7e (RSA)
|   256 93:55:b4:d9:8b:70:ae:8e:95:0d:c2:b6:d2:03:89:a4 (ECDSA)
|_  256 f0:61:5a:55:34:9b:b7:b8:3a:46:ca:7d:9f:dc:fa:12 (ED25519)
80/tcp    open   http       Apache httpd 2.4.37 ((centos) OpenSSL/1.1.1c)
|_http-title: Did not follow redirect to https://thomaswreath.thm
|_http-server-header: Apache/2.4.37 (centos) OpenSSL/1.1.1c
443/tcp   open   ssl/http   Apache httpd 2.4.37 ((centos) OpenSSL/1.1.1c)
|_ssl-date: TLS randomness does not represent time
|_http-title: Thomas Wreath | Developer
| tls-alpn: 
|_  http/1.1
| ssl-cert: Subject: commonName=thomaswreath.thm/organizationName=Thomas Wreath Development/stateOrProvinceName=East Riding Yorkshire/countryName=GB
| Not valid before: 2023-12-06T04:50:11
|_Not valid after:  2024-12-05T04:50:11
|_http-server-header: Apache/2.4.37 (centos) OpenSSL/1.1.1c
| http-methods: 
|_  Potentially risky methods: TRACE
9090/tcp  closed zeus-admin
10000/tcp open   http       MiniServ 1.890 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
Aggressive OS guesses: HP P2000 G3 NAS device (89%), Linux 2.6.32 (88%), Linux 2.6.32 - 3.1 (88%), Ubiquiti AirMax NanoStation WAP (Linux 2.6.32) (88%), Linux 3.7 (88%), Linux 5.0 (88%), Linux 5.0 - 5.4 (88%), Linux 5.1 (88%), Ubiquiti AirOS 5.5.9 (88%), Ubiquiti Pico Station WAP (AirOS 5.2.6) (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 9090/tcp)
HOP RTT       ADDRESS
1   155.54 ms 10.50.86.1
2   155.62 ms 10.200.85.200

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Dec  6 00:05:42 2023 -- 1 IP address (1 host up) scanned in 128.80 seconds

```

