
What is C2 (command and control)
C2 framework are used to consolidate an attacker's positions within a network and simply post-exploitation steps (privesc, AV evasion, pivoting, looting, covert network tactics, etc), 
as well as providing red teams with extensive collaboration features.

Cobalt Strike
https://www.cobaltstrike.com/

Will be looking into both Empire and it's GUI extension: "Starkiller". 
It's been split into a server mode and a client mode.


Installation
```
sudo apt install powershell-empire starkiller
```


Starting Empire Server
```
sudo powershell-empire server
```

![[Pasted image 20231230194435.png]]


Starting Empire Client
```
powershell-empire client
```
![[Pasted image 20231230194813.png]]

```
http://localhost:1337/index.html
```
![[Pasted image 20231230194927.png]]

```
empireadmin
```

```
password123
```


Listeners 
Stagers 
Agents
Modules 

Setting up Empire and Starkiller using the already compromised Webserver as a target. 
Once we have a handle on how Empire operates, we will switch focus to our primary target: the Git Server.

