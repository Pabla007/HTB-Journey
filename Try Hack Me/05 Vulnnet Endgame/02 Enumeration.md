
![[Pasted image 20231126151139.png]]

So we have to add the above domain in the hosts file.

```
http://vulnnet.thm/
```
![[Pasted image 20231126151320.png]]


## silence is eloquence

![[Pasted image 20231126152051.png]]



```
 nikto -h vulnnet.thm              
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.10.243.58
+ Target Hostname:    vulnnet.thm
+ Target Port:        80
+ Start Time:         2023-11-26 04:44:44 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/2.4.29 (Ubuntu)
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ /: Server may leak inodes via ETags, header found with file /, inode: 10fa, size: 5e07a2716f080, mtime: gzip. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2003-1418
+ Apache/2.4.29 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ OPTIONS: Allowed HTTP Methods: OPTIONS, HEAD, GET, POST .
+ /css/: This might be interesting.
+ /images/: Directory indexing found.
+ /icons/README: Apache default file found. See: https://www.vntweb.co.uk/apache-restricting-access-to-iconsreadme/
+ 7962 requests: 0 error(s) and 8 item(s) reported on remote host
+ End Time:           2023-11-26 05:09:22 (GMT-5) (1478 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

Vulnnet subdomains
```
http://admin1.vulnnet.thm/en/
http://blog.vulnnet.thm/author.html?
http://api.vulnnet.thm/
http://shop.vulnnet.thm/index.html
```

![[Pasted image 20231126163009.png]]
![[Pasted image 20231126163455.png]]


```
wfuzz -u vulnnet.thm -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt  -H "Host:FUZZ.vulnnet.thm"
```
![[Pasted image 20231126160842.png]]

As you can see we have different Ch value means we can use -hh 65 
which means that we can filter the chars using -hh
```
wfuzz -u vulnnet.thm -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt  -H "Host:FUZZ.vulnnet.thm" --hh 65
```
![[Pasted image 20231126164938.png]]


![[Pasted image 20231126162643.png]]

![[Pasted image 20231126162657.png]]

![[Pasted image 20231126162837.png]]

![[Pasted image 20231126162848.png]]

