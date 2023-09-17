nmap -T4 -p- -A www.moshai.in  
Starting Nmap 7.92 ( https://nmap.org ) at 2023-08-09 00:43 IST
Nmap scan report for www.moshai.in (23.227.38.74)
Host is up (0.0043s latency).
rDNS record for 23.227.38.74: shops.myshopify.com
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE    VERSION
80/tcp   open  tcpwrapped
|_http-server-header: cloudflare
443/tcp  open  tcpwrapped
|_http-server-header: cloudflare
| tls-alpn: 
|   h2
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
| tls-nextprotoneg: 
|   h2
|_  http/1.1
|_http-title:       Moshai India - Fabrics for every Indian Man                                                                                                                              
| ssl-cert: Subject: commonName=www.moshai.in                                                                                                                                                
| Subject Alternative Name: DNS:www.moshai.in
| Not valid before: 2023-07-31T03:09:56
|_Not valid after:  2023-10-29T03:09:55
8080/tcp open  tcpwrapped
|_http-server-header: cloudflare
|_http-title: Attention Required! | Cloudflare
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Aastra 480i IP Phone or Sun Remote System Control (RSC) (88%), Aastra 6731i VoIP phone or Apple AirPort Express WAP (88%), Crestron MPC-M5 AV controller or Wago Kontakttechnik 750-852 PLC (88%), Konica Minolta bizhub 250 printer (88%), Brother MFC-7820N printer (87%), Sony Ericsson U8i Vivaz mobile phone (87%), Netgear SC101 Storage Central NAS device (86%), Digi Connect ME serial-to-Ethernet bridge (86%), Nokia 3600i mobile phone (85%), Apple Time Capsule NAS device (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 80/tcp)
HOP RTT     ADDRESS
1   0.11 ms 192.168.17.2
2   0.14 ms shops.myshopify.com (23.227.38.74)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 225.73 seconds



@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@┌──(root㉿kali)-[~]
└─# nmap -sS -T4 -p- -A moshai.in 
Starting Nmap 7.94 ( https://nmap.org ) at 2023-08-30 03:33 EDT
Nmap scan report for moshai.in (23.227.38.32)
Host is up (0.0019s latency).
rDNS record for 23.227.38.32: myshopify.com
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE    VERSION
80/tcp open  tcpwrapped
|_http-title: Did not follow redirect to https://www.moshai.in/
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: phone|VoIP phone|remote management|WAP|media device|specialized|printer
Running (JUST GUESSING): Nokia Symbian OS (86%), Aastra embedded (85%), Sun embedded (85%), Apple embedded (85%), Crestron embedded (85%), Wago Kontakttechnik embedded (85%), Konica Minolta embedded (85%)
OS CPE: cpe:/o:nokia:symbian_os cpe:/h:apple:airport_express cpe:/h:crestron:mpc-m5 cpe:/h:wago_kontakttechnik:750-852 cpe:/h:konicaminolta:bizhub_250
Aggressive OS guesses: Nokia 3600i mobile phone (86%), Aastra 480i IP Phone or Sun Remote System Control (RSC) (85%), Aastra 6731i VoIP phone or Apple AirPort Express WAP (85%), Crestron MPC-M5 AV controller or Wago Kontakttechnik 750-852 PLC (85%), Konica Minolta bizhub 250 printer (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 80/tcp)
HOP RTT     ADDRESS
1   0.09 ms 192.168.17.2
2   0.12 ms myshopify.com (23.227.38.32)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 175.37 seconds


########################################################################

