
As you can see that we are not able to load the page fully 
![[Pasted image 20240810102758.png]]

Which means that we need to add the IP address in our localhost and see the magic

```
whatweb 10.201.11.33
http://10.201.11.33 [200 OK] Apache[2.4.29], Country[RESERVED][ZZ], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.29 (Ubuntu)], IP[10.201.11.33], MetaGenerator[WordPress 5.5.3], Script[text/javascript], Title[holo.live], UncommonHeaders[link], WordPress[5.5.3], X-UA-Compatible[IE=edge]
```

We were able to see from the nmap scan that we are able to access the robots.txt
```
http://www.holo.live/robots.txt
```
![[Pasted image 20240810164134.png]]

