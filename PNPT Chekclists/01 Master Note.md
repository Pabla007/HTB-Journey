
<h2>Nmap</h2>

Normal Nmap Scanning
```
nmap -T4 -p- -A -Pn <IP_Address>
```

```
nmap -sS -T4 -p- -Pn <IP_Address>
```


Ping Sweep
```
nmap -sn -n 10.200.95.0/24 -oA Ping-Sweep
```

```
nmap -sS 10.200.145.33 10.200.145.250 -v -oA Initial-Scan-Subnet1-Hosts
```



<h2>Fuzzing</h2>
>[!important]  Gobuster

Vhost
```
gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://<IP_Address> -o gobuster/vhost-sub.txt -t 2
```

```
gobuster vhost -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt -u http://<IP_Address> -t 2 -o gobuster/vhost-sub.txt
```



>[!important] Wfuzz
```
wfuzz -u <URL> -w <wordlist> -H "Host: FUZZ.example.com" --hc <status codes to hide>
```

```
wfuzz -u http://<Hostname> -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt  -H "Host: FUZZ.<hostname>" --hc 400
```

```
--hc Hide status code
--hw Hide word count
--hl Hide line count
--hh Hide character count
```


>[!important] ffuf
```
ffuf -u http://holo.live -w /usr/share/wordlists/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt -H "HOST:FUZZ.holo.live" -mc 200 -o fuzz_holo.txt
```



>[!important] 


<h2>Sub-Domains</h2>
Sublist3r
```
sublist3r -d <domain_name> -t 100
```

Amass
```
amass enum -d tesla.com 
```

```
amass intel -d tesla.com -whois
```

Httpprobe
```
cat domains.txt | httprobe >> working_domains.txt
```


<h2>Enumeration</h2>
```
wpscan -url <IP_address>    
```


```
whatweb <domain_name>
```

