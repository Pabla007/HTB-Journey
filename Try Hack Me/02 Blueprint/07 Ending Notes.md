We have to reconnaissance and by doing it we found there are 4 vulnerabilities that we could try with 
oscommerce 2.3.4 when we used Searchsploit
RCE and File Upload

We have gone with File Upload as it doesn't use Metasploit
Simply we have found the url and simply run the directory bustor and got to know about install

Simply we have gone to website and saw that the server could be installed as a root aka admin user which we could exploit and make use in our favor

Simply uploaded a cmd shell using PHP which will use to trigger the windows shell.exe than will upload after this

Will use msfvenom to make this payload and simply upload it
Once it got upload will try to get the reverse shell which we got and simply try to run the Mimikatz and get the sam dump and simply cracked one user password using crack station 

And got the root flag afterwards.

Learned 
Reconnaissance
Malware upload through attacker server (i.e. From Linux to Windows server)

