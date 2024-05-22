
```
Want to adjust the threat or risk of an individual IP address? Set up a Host Record!
```


Host Records identify individual hosts.

This allows you to individualize risk and threat ratings  
(overriding Network Record defaults).

![[Pasted image 20240516144108.png]]


**A Host Record identifies an individual host, so it must contain a unique identifier**  
(IP address, host name, and/or DNS name) when being created. From there:

- **It can be assigned its own risk and threat ratings** (which will override its originally prescribed network record ratings). 
- If no rating is given to a Host Record, **it will inherit risk and threat ratings** (if the host IP falls within a range defined by a Network Record).

Ultimately, Host Records allow for **pinpoint accuracy** in the weighted importance of log information that comes from that host’s Log Source.


## What's the difference? Assets vs. Known Hosts vs. Unknown Hosts


Definitions: Assets- At times, LogRhythm refers to hosts as "assets"  
  
Known Hosts are Host records defined in an Entity. 

***Unknown Hosts** are machines/devices that we are not collecting logs from.  
Unknown hosts are often identified within log messages from other Log Sources (such as firewalls, routers, switches, or from other host computers such as domain controllers, email servers, or web servers). These Unknown Hosts may include devices such as tablets, smart phones, or laptops that are performing activities on your network.


## What about hosts that we're not collecting logs from?

**A Network record can be used to assign Risk and Threat to "Unknown Hosts"** (machines/devices that we are not collecting logs from).

Even though they are unknown to LogRhythm, these hosts can still (usually) have Risk and Threat rating values assigned simply because they exist within one of your specified Network records. 

The Risk and Threat values defined in Network records help to define the weighted importance of these Unknown Hosts.  
  
The assigned Risk and Threat values for these hosts are assigned automatically based on the Network in which they reside. Risk and Threat are used to determine the RBP values assigned to logs in which information about these Unknown Hosts is included.


>[! question] Regardless of the setup, **Host Records _must_ contain a unique identifier**   
(IP address, host name, and/or DNS name) when being created.

