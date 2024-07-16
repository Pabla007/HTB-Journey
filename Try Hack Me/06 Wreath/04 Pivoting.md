
Pivoting is the art of using access obtained over one machine to exploit another machine deeper in the network. It is one of the most essential aspects of network penetration testing, and is one of the three main teaching points for this room.

![[Pasted image 20231216204015.png]]

Manual Techniques For Pivoting:
Tunnelling/Proxying:
Tunneling of pivoting creates a channel through which information can be sent hidden inside another protocol
SSH tunnelling, which can be useful for evading a basic **I**ntrusion **D**etection **S**ystem (IDS) or firewall

Port Forwarding
Creating a connection between a local port and a single port on a target, via a compromised host

## Always starting drawing the layout of a network as you get further it will give as a sense of how the network is working

```
The remaining tasks in this section will cover the following topics:

- Enumerating a network using native and statically compiled tools
- Proxychains / FoxyProxy
- SSH port forwarding and tunnelling (primarily Unix)
- plink.exe (Windows)
- socat (Windows and Unix)  
    
- chisel (Windows and Unix)
- sshuttle (currently Unix only)
```

Portforwarding in Detail:
https://www.offsec.com/metasploit-unleashed/portfwd/

- Linux systems sometimes have Nmap installed by default, this is an example of Living off the Land (LotL) -- a good way to minimize risk
- misconfigured to allow something like a DNS zone transfer attack
windows : 
```
ipconfig /all
```
Linux:
```
nmcli dev show
```


DNS file location :
```
Linux -- /etc/resolv.conf
Windows -- C:\Windows\System32\drivers\etc\hosts
for i in {1..225}; do (ping -c 1 172.16.0.${i} | grep "bytes from" &); done 
```


Proxy Chains
```
cat /etc/proxychains.conf 
```
![[Pasted image 20231216223620.png]]

Proxy_Dns
![[Pasted image 20231216224120.png]]


<h2>Pivoting Blog </h2>
https://theyhack.me/Proxychains-Double-Pivoting/
How to access a network if it has internal access ?
or
Does it have access to another machine ?
or
Each of this machine is restricted by a host-based firewall 

Will use 
ssh along with proxychains4
![[Pasted image 20231219065933.png]]

How will we talk to destbox.local than ??
Sock Proxies : A sock proxy difers from traditional port forwarding in that sock is a protocol,
whereas forwarding is routing.

OSI Layer:
Port forwarding happening in the network layer (i.e. send any traffic over a port forward: ssh traffic, http traffic, raw bytes.........)
while
Socks proxying works at the application layer (i.e. communication will occue using the defined protocol)

1st machine (Attacker to Jumpbox1)
SOCK proxy b/w 2 machines:
ssh -f -N -D 127.0.0.1:8888 user@jumpbox1.local

Once the Socks proxy established we can than use proxychains4 to communicate over the newly established tunnel/proxy.

SOCK proxy b/w 2 machines: (Jumpbox1 to Jumpbox2)
ssh -f -N -D 127.0.0.1:9999 user@jumpbox1.local
Keep in mind that the proxychains4 is going to use each proxy in a ordered list approach.

Finally we can talk Attacker to Destbox
proxychains4 -f ~/new-proxychains.conf curl http://destbox.local

Note** that we are using strict chain that means if one fails than proxy chains won't work.
But we can also use Dynamic chain that menas if one fails than it will move to the next one.

<h2>Wait what we can't SSH to a box like jumpbox1 in our case</h2>
- There will be a time when we will be having a shell access but will not able to do ssh on that box. And the box didn't want to get exposed to the world.
- SSH reverse tunnel is the solution

>[!note] Terms Made Easy To Learn and Understand

<h2>Port Fowarding</h2>
With port forward you tell the mailman to temporarily send your letters to a friend in apartment 404.
Your friend then forwards the letter to you.  
It's like rerouting data through a specific port to reach it's destination.

<h2>Pivoting</h2>
Pivoting is like a Secret Tunnel inside that apartment building.
We are in an apartment 305 and you have to visit your friend in apartment 404 without going through the main Hallway.
It's creating a hidden path b/w computers to access them without going the regular routes. 
It's like a taking a shortcut through a secret passage.

<h2>Jump Server</h2>
It's referred to a jump host or jump box, is like a security checkpoint for your computer network.

Security Guard : The jump server acts like a security guard at the castle gate.
Control Center : Instead of allowing direct access to every computer that you use to manage and control access to other computers in your network.
Protection : It adds an extra layer of protection.

