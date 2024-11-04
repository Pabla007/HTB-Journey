Will use John2Zip to see what is inside the locked zip aka would simply peek inside

```
- zip2john experiment_gone_wrong.zip > hash123.txt
- john --wordlist=/usr/share/wordlists/rockyou.txt hash2.txt
- unzip experiment_gone_wrong.zip
```

```
 unzip experiment_gone_wrong.zip
```
![[Pasted image 20230920154136.png]]
So there are 2 flies inside and both are sensitive files as well a both are password protected.

```
zip2john experiment_gone_wrong.zip > hash.txt
```
![[Pasted image 20230920154257.png]]

```
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```
![[Pasted image 20230920154500.png]]

I think before the zip file was corrupt or something or i have been passing wrong code.

Even Fcracked also worked this time hahahaha
```
fcrackzip -v -u -D -p /usr/share/wordlists/rockyou.txt experiment_gone_wrong.zip
```
![[Pasted image 20230920154638.png]]

Password: electromagnetismo
```
electromagnetismo
```


So let's unzip the zip file
![[Pasted image 20230920154906.png]]


```
bloodhound-python -d raz0rblack.thm -u sbradley -p hackingakatesting -ns 10.10.43.122 -c all
```

![[Pasted image 20230920160056.png]]

