
```
http://10.200.95.33/
or
http://www.holo.live/
```
![[Pasted image 20230926225104.png]]

```
wpscan -url 10.200.95.33    
```
![[Pasted image 20231001215314.png]]


Directory Busting aka Gobuster
```
gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://10.200.95.33 -o gobuster/vhost-sub.txt -t 2

gobuster vhost -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt -u http://holo.thm -t 2 -o gobuster/vhost-sub.txt
```
![[Pasted image 20230926235313.png]]
![[Pasted image 20230926235632.png]]
![[Pasted image 20231001200601.png]]
The output is being stored in the txt file so we ca grep it easily later.
Gobuster didn't worked in this case 

So will either go with FFUF or Wfuzz both will work fine
```
ffuf -u http://holo.live -w /usr/share/wordlists/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt -H "HOST:FUZZ.holo.live" -mc 200 -o fuzz_holo.txt
```


Now that we have some vhosts to work off from fuzzing, we need a way to access them. If you're in an environment where there is no DNS server, you can add the IP address followed by the FQDN of the target hosts to your _/etc/hosts_ file on Linux or _C:\\Windows\\System32\\Drivers\\etc\\hosts_ file if you're on Windows.

**Important** thing to learn is how Vhosts works in this scenario and how it differ's from Directory bursting.

We can utilize Gobuster again to identify potential vhosts present on a web server. 
The syntax is comparable to fuzzing for directories and files; however, we will use the `vhosts` mode rather than `dir` this time. 
`-u` is the only argument that will need a minor adjustment from the previous fuzzing command. 
`-u` is the base URL that Gobuster will use to discover vhosts, so if you provide `-u` "
[https://tryhackme.com](https://tryhackme.com/)" 

GoBuster will set the host to "[tryhackme.com](http://tryhackme.com/)" and set the host header to `Host: LINE1.tryhackme.com`.
If you specify "[https://www.tryhackme.com](https://www.tryhackme.com/)", 
GoBuster will set the host to "[www.tryhackme.com](http://www.tryhackme.com/)" and the host header to `Host: LINE1.www.tryhackme.com`. Be careful that you don't make this mistake when fuzzing.

VHOST proper explanation
```
#### Virtual host (vhost)

A virtual host (vhost) is used as a wrapper for the domain itself, it can be the top-level domain, or a sub-level of a top-level domain.

Virtual hosts have their own configurable Nginx rewrite and configuration files, the configuration files used for that top-level domain is shared amongst all of its subdomains.

Virtual hosts do not have to be a top-level domain (eg. `example.com`), they can also be a sub-level domain of that (eg. `dev.example.com`). This is useful when you need a separate Nginx configuration file for a subdomain from that of the top-level domain - without the need to use conditional statements. There is no limit to the depth of a virtual host domain (eg. `my.test.dev.example.com`).
```

Nikto
```
http://holo.live/
```
![[Pasted image 20230927003235.png]]



Got this data in Nmap scan but verified it
```
http://10.200.95.33/robots.txt
User-Agent: *
Disallow: /var/www/wordpress/index.php
Disallow: /var/www/wordpress/readme.html
Disallow: /var/www/wordpress/wp-activate.php
Disallow: /var/www/wordpress/wp-blog-header.php
Disallow: /var/www/wordpress/wp-config.php
Disallow: /var/www/wordpress/wp-content
Disallow: /var/www/wordpress/wp-includes
Disallow: /var/www/wordpress/wp-load.php
Disallow: /var/www/wordpress/wp-mail.php
Disallow: /var/www/wordpress/wp-signup.php
Disallow: /var/www/wordpress/xmlrpc.php
Disallow: /var/www/wordpress/license.txt
Disallow: /var/www/wordpress/upgrade
Disallow: /var/www/wordpress/wp-admin
Disallow: /var/www/wordpress/wp-comments-post.php
Disallow: /var/www/wordpress/wp-config-sample.php
Disallow: /var/www/wordpress/wp-cron.php
Disallow: /var/www/wordpress/wp-links-opml.php
Disallow: /var/www/wordpress/wp-login.php
Disallow: /var/www/wordpress/wp-settings.php
Disallow: /var/www/wordpress/wp-trackback.php
```
![[Pasted image 20230927002341.png]]

nmap -sn -n 10.200.95.0/24 -oA Ping-Sweep

10.200.95.33
10.200.95.250

nmap -sS 10.200.95.33 10.200.95.250 -v -oA Initial-Scan-Subnet1-Hosts

Remember that we don't have to use www here keep that in mind 
```
wfuzz -u http:holo.live -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt  -H "Host: FUZZ.holo.live" --hc 400
```

![[Pasted image 20231001215759.png]]

i don't know but i didn't got any vhost using gobuster.

Remember in order to access the admin or dev site that we have found above we have to add them in the host file otherwise they will not load.
![[Pasted image 20231005192407.png]]


http://admin.holo.live/
![[Pasted image 20231005192253.png]]

http://dev.holo.live/
![[Pasted image 20231005192335.png]]

