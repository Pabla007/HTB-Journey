Ffuf
```
ffuf -w /usr/share/wordlists/dirb/common.txt:FUZZ -u http://holo.live//FUZZ   
```

Normal site leak file will explore it later
![[Pasted image 20231005202917.png]]

Admin site
Gobuster
```
gobuster dir -u http://admin.holo.live/ -w /usr/share/wordlists/seclists/SecLists-master/Discovery/Web-Content/big.txt -t 30
```
![[Pasted image 20231005205034.png]]

http://admin.holo.live/robots.txt
![[Pasted image 20231005205142.png]]
```
User-agent: *
Disallow: /var/www/admin/db.php
Disallow: /var/www/admin/dashboard.php
Disallow: /var/www/admin/supersecretdir/creds.txt
```



http://dev.holo.live/img.php?file=images/matsuri.jpg
![[Pasted image 20231005202847.png]]
![[Pasted image 20231005202807.png]]

