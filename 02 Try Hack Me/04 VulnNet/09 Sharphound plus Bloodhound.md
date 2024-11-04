Start the neo4j and bloodhound 
Simply run the bloodhound and get it using the smb share file in my system
than simply extract and uploaded the data in the bloodhound
![[Pasted image 20230917211041.png]]

I tried to run winpeas but was not able to run it due to some reason.

Let's see what juicy data we get from here.
Now will run some query and see what we get from here
![[Pasted image 20230917212016.png]]

Shortest path to the admin 
![[Pasted image 20230917212321.png]]

![[Pasted image 20230917212548.png]]
On Zooming we got to know that enterprise-security has generic write permission. (i.e. SECURITY-POL-VN@VULNNET.LOCAL to be precise)

![[Pasted image 20230917212735.png]]

```
Since we have _GenericWrite_ privileges on the **SECURITY-POL-VN** GPO, [**SharpGPOAbuse**](https://github.com/FSecureLABS/SharpGPOAbuse) or [**PowerView**](https://github.com/PowerShellMafia/PowerSploit/blob/26a0757612e5654b4f792b012ab8f10f95d391c9/Recon/PowerView.ps1#L5907-L6122) can be used to abuse these privileges and create a malicious scheduled task.
```




