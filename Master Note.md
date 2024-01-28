
<h2>Nmap</h2>
```
nmap -sn -n 10.200.95.0/24 -oA Ping-Sweep
```


```

```

<h2>Enumeration</h2>
```
wpscan -url <IP_address>    
```

<h2>Fuzzing</h2>
>[!important]  Gobuster

>[!important] Wfuzz
```
wfuzz -u <URL> -w <wordlist> -H "Host: FUZZ.example.com" --hc <status codes to hide>
```



>[!important] 

