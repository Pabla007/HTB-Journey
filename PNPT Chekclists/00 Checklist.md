
This is a check list so that i don't forget something while Pen testing and it will change with Time.



<hr>


<h2>Exam Strategy / Things to look</h2>
- [ ]  Think like an Hacker and not a CTF mindset
- [ ] Look for Misconfiguration (i.e. Recycle bin , Browser History , temp folder like that)
- [ ] Out of the Box 
- [ ] OSINT
- [ ] Buffer Overflow
- [ ] Pivoting
- [ ] AD Attack
- [ ] AV Evasion
- [ ] Looks for latest CVE or previous one



<hr>



Things needed to setup up before the exam:
- [ ] windows 7/10 for performing buffer overflow attack (i.e. install the required software and scripts)
- [ ] Payload (i.e. All the payloads for both windows and Linux in place)
- [ ] Cheatsheets
- [ ] [CyberChef](https://gchq.github.io/CyberChef/)



<hr>


<h2> Initial Steps</h2>
Verify the IP address:
- [ ] Always check the [Website](https://bgp.he.net/) before starting the PT

Add the IP to the host files
- [ ] Open the IP address in the web-browser before adding it to the host files



<hr>



<h2> Information Gathering</h2>
- [ ] Identify targets
- [ ] Email Enumeration 
- [ ] Web Enumeration 
- [ ] Google Fu



<hr>


<h2> Scanning / Enumeration</h2>
- [ ] Nessus (i.e. this is the 1st thing we should do when got the ip cuz it will take time)
- [ ] Nmap 
- [ ] Dnsrecon 
- [ ] arpscan (i.e. when we got a reverse shell )
- [ ] Nikto 
- [ ] Wappalyzer
- [ ] Vhost
- [ ] Directory Bursting
- [ ] wpscan
- [ ] Searchspolit
- [ ] 

Note* that some of the list below will not applicable as it totally depends on the port.
```
- Will target the low hanging fruits.
- 80 > 443 > 139 > 445 are the juicest of all.
```


<hr>



<h2> Active Directory</h2>
- [ ] kerbrute
- [ ] evil-winrm



<hr>


<h2> Privilege Escalation</h2>
- [ ] Privilege escalation
- [ ] GTFObins
- [ ] PEASS-ng (Winpeas , Linpeas)
- [ ] pspy



<hr>



<h2>Windows</h2>



<hr>


<h2>Linux</h2>


<hr>


<h2>Zip File</h2>
Fcrackzip


<hr>


### Other resource that would might come as handy

 One of the most prominent of these is [Payloads all the Things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md). 
 
 The PentestMonkey [Reverse Shell Cheatsheet](https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) is also commonly used. 
 
 In addition to these online resources, Kali Linux also comes pre-installed with a variety of webshells located at `/usr/share/webshells`. 
 
 The [SecLists repo](https://github.com/danielmiessler/SecLists), though primarily used for wordlists, also contains some very useful code for obtaining shells.


