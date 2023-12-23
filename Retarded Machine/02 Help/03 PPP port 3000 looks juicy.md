![[Pasted image 20230725190828.png]]

{"message":"Hi Shiv, To get access please find the credentials with given query"}

When trying this got this error http://10.10.10.121:3000/application/json
![[Pasted image 20230725191105.png]]

http://10.10.10.121:3000/graphql
![[Pasted image 20230803124357.png]]When trying to run this we are getting a query missing error.
to get the missing query we search on google pentest graphql
query={__schema{types{name,fields{name,args{name,description,type{name,kind,ofType{name, kind}}}}}}}


When we run the following query we get this
![[Pasted image 20230803131052.png]]

When we run this query and intercept we got this output
![[Pasted image 20230803131953.png]]

![[Pasted image 20230803132050.png]]
"username":"helpme@helpme.com","password":"5d3c93182bb20f07b994a7f617e99cff"

And when run it in the hashes.com we were able to find the password
![[Pasted image 20230803132524.png]]

Now we will put the username and password in the login page and see what happens
Username and password
helpme@helpme.com
godhelpmeplz

![[Pasted image 20230803133216.png]]
