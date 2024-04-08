
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
openssl req -newkey rsa:2048 -nodes -keyout request.key -out request.csr
```
![[Pasted image 20240408133614.png | 500]]

```
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQC3Olvi6uGdfvyi
yKtQ9FG53NTpztb8pboL6npJaRnHk3Tgf4EFZA5FI6f5xaBaHKBJTAHNNc2tzeRI
Q3jSki5MTv38r6iNpU1f/1KrxTCa894KD4hlnbqJeyxAJ/LLYpanIPz0BjIZaS6u
49zFn2miaGhLsrFdJCQWe9MVxEN09ybvFHRJaTVpN9nay6w4xnMNnYtQ9hf2Q1OA
reQ2yr7w+Y6HHOWjv/W5fgPSwv4YRAmo4fn4GlzUF4dvmbQr0pi0exmmdgkQUNM/
ZVj40E5VdCniz2cXMSAdx8xnTF6/4bNfil/i7LLUDmoZXLoKVkUSzMkD759PW8CA
BunxFaIVAgMBAAECggEAHjy6AbRX170nVXjOts0e+JBuLYiGF4sE7Sb8l8VJrRMT
SGIaSWi15yiHdbNsrzpGpFnv+SzOHMbby6Yg2AUqMUse5JabdwamwncY7kJcL1Ib
3CaskHJrYHlMd+jvyyshqAKMY/vqxCFExDVTz2Qrk1LuFUHvvapzbydvkgnBxRkl
w+KYOjwbGX+ERNUaoYLn+H334e8jRfz2LEN80ebMCIFKtaWicwz/f/EVLMvt+JEh
LqjUX62F9BZXIm0qZg5+LWhCYg3ny521NowuSKNtRuTDPBohe3gN+qtwbpQMIFOg
4Xm4eMQpYVbsnilKvGuUkzIub3JqjU0g2XdzM8Rz0QKBgQDkpnoq14Y8u2/a1YbD
Vtvop0/LeJaIDsy0pcODb9ofbIkf2XsUFZl9xBYT/9Ffn/0AYne3lH5gJltzAI5e
lMnScepX0cwcxckWl1RkcL9iaarOUKmyRBrax6cwu4GXaUIXqRzVPstF71k+YzlM
j2CK3g0VHNVEPVUGII72ve9BEQKBgQDNJP/+1A6fkdFmFyk3Ydpo5ZGDs4q2zB/i
BShDEtL3PnxecR9qrgqSbGUBPgUQUWubWW8RzLzF7r57p06uMEErVaCgivouP3PU
D3RhWp6+enVOsoyWVDaioKY2a8hAwIxAvUWqEFF/CWCptld7JRakGO4g/vveUqjd
qb6mLW+QxQKBgFdH+VCLTxG11x/o7HV6nZ106K/aC1RKmffHYxe0RcZDDyEaSrJD
AIGSrX7a41imYNSZwetRAuC/I5+FsdMG5vevRm5ZhpnhIj6+a5eftl7hyTLSdcS3
3KxxFDA1E2Xx5ynTA0+flcbPc/ittby06nx4APRzOjG/W8pn+UrU/BSRAoGBAMYk
aq5zm/w8F4kH7eN0PET9F2Oh0uVkm5bvbEf8so/kZrPBh5q+p69tytE8Wh+8xLaz
1zfWDK8RPiKpIrHUId39QrxN//8TgojctIgjwxgvp4ZvpqK8jFjf2irOSAli8RTG
u7bbNBwDrr29RRnIZOnyum5cWmIObNRM07wmPpARAoGBAJTtaosH29iGJihz2XR+
aXIdAAigFvjLxF4OJIhqPPf8yEL3/gw6codmvpT60R/9DgWLMfHoYIUY+Tbhaw/I
2yj9bTieWSxkYeOPhZ51+yVxDDefxx0HBcH7kCOm6ous+ICluA7HfAIZxW7tba2g
cshSaN8SxbPojYzP996FLBIV
```

