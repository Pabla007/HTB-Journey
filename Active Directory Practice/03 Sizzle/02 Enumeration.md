
![[Pasted image 20231119231622.png]]

```
gobuster dir -u http://10.10.10.103 -w /usr/share/wordlists/dirb/common.txt

/aspnet_client        (Status: 301) [Size: 157] [--> http://10.10.10.103/aspnet_client/]
/certenroll           (Status: 301) [Size: 154] [--> http://10.10.10.103/certenroll/]
/certsrv              (Status: 401) [Size: 1293]
/images               (Status: 301) [Size: 150] [--> http://10.10.10.103/images/]
/Images               (Status: 301) [Size: 150] [--> http://10.10.10.103/Images/]
/index.html           (Status: 200) [Size: 60]

```
![[Pasted image 20231119233234.png]]

