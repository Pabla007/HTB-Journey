Objective

Your task is to make the current user change their own password, without them knowing about their actions, using a CSRF attack.


>[!important] Security is Set to Low

Will simply test the change password functionality and interrupt the traffic with Burp Suite and will see what's happening behind the scenes.
![[Pasted image 20231014190539.png]]
![[Pasted image 20231014190752.png]]

I suspect that is the link that is what we are after let's test it and again change the password to password.
```
/DVWA/vulnerabilities/csrf/?password_new=test&password_conf=test&Change=Change
```

Yes my hunch was correct and we are able to change the password through this link
![[Pasted image 20231014191139.png]]

So this is the link we will simply send the victim so that the person could simply click on this link and Volla mission complete......................


>[!important] Let's now change the level to medium and will see if any check are being happening now:

I have gone through the help section now they are checking for some king of authentication if the request is coming from the trusted source or not
```
http://localhost/DVWA/vulnerabilities/csrf/?password_new=test123&password_conf=test123&Change=Change#
```
![[Pasted image 20231014193730.png]]

Now  Reference is Missing 
![[Pasted image 20231014193943.png]]
![[Pasted image 20231014194037.png]]

Before in low security we have reference 
![[Pasted image 20231014194011.png]]

So here we have to take the help of XSS stored vulnerability and simply add the request in the image and from there the change will be triggered. 
But will set the security to low for XSS 
```
<img scr="localhost/DVWA/vulnerabilities/csrf/?password_new=test123&password_conf=test123&Change=Change#">
```
![[Pasted image 20231014200025.png]]

Now will change the security to medium and test the password
Password changed to test123 successfully
![[Pasted image 20231014200134.png]]



>[!important] Let's change the level to High

As you can see that the user_token has been added in the high security 
![[Pasted image 20231014201305.png]]

If you go through the source
![[Pasted image 20231014202232.png]]
We can see that there's a user token but the question is that how to get it

So the code is
```
document.getElementsByName("user_token")[0].value 
"0e5a3f410f4b9cced9ff3a2fefafe718" 
```


Will simply send the code in the XSS and we know that we need to send the token and we know how to get it so let's change the password
```
<img scr="localhost/DVWA/vulnerabilities/csrf/?password_new=test123&password_conf=test123&Change=Change&user_token="+document.getElementsByName("user_token")[0].value>
```

But we are not able to do it as the security is high for Xss as well no point of doing the security to low and fire up the attack in order to change the password.


So the solution is if we have access to the XSS stored than we can simply have the user token from their and than send the user link in order to trick him like have u heard about this news and if the person clicks on the link bomb the attack is executed. So there should be contribution from the user as well so get this attack to be executed.