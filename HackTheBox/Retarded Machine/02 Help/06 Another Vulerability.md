This is what we are able to see after we login with user and id
helpme@helpme.com
godhelpmeplz
![[Pasted image 20230813115419.png]]

![[Pasted image 20230813115522.png]]
We get a ohk request when we were trying to find if sql injection is possible or not and yes it is

![[Pasted image 20230813121106.png]]

It looks like it is Boolean based sql injection
![[Pasted image 20230813121237.png]]

Will put the request in helpdeskz.req and run the sqlmap on it
sqlmap -r helpdeskz.req --batch

![[Pasted image 20230813122354.png]]
