
```
This is the fifth way that Log Sources can be onboarded within LogRhythm.
```

## Syslog & Syslog Relay


### Syslog: 

- Stands for **System Logging Protocol**.
- Is a standard protocol used to send system log or event messages to a specific server, called a syslog server.  

- **Is a framework for log generation, storage, and transfer, using various operating systems**, though it is normally associated with *Nix technologies.
- Is primarily used to collect various device logs from several different machines in a central location for monitoring and review.



## Priority & Message parts

**Syslog Priority**  
Syslog Format assigns a priority to each log message based on importance of the following attributes:

1. **Message Type**, known as a facility (e.g. kernel messages, authorization messages, audit messages)
2. **Severity** – each log message has a value from 0 (emergency) to 7 (debug)

It uses this message priority to determine the order of message handling – i.e., forwarding higher-priority messages more quickly than lower priority messages.  


**Parts of a Syslog Message** 

Syslog packet transmission is asynchronous. The syslog message consists of three parts: 

- PRI - a calculated priority value
- HEADER - with identifying information
- MSG - the message itself


## UDP or TCP

Syslog can be sent as UDP or TCP. Most Firewalls will send their logs as UDP, as they will not want the overhead of maintaining TCP state tables for Syslog. 

  
Traditionally, Syslog uses the UDP protocol on port 514 but can be configured to use any port. In addition, some devices will use TCP 1468 to send syslog data to get confirmed message delivery.




>[! bug] ## Limitations

One major limitation of the syslog protocol is that the device being monitored must be up and running and connected to the network to generate and send a syslog event. 

A critical error from the kernel facility may never send an error at all as the system goes offline. **In other words, syslog is not a good way to monitor the status of devices**.


<hr>

### Syslog Relay Host

>What is a Syslog Relay Host ?

A Syslog Relay Host, or Syslog aggregator, is a device that will accept Syslog messages from many different Log Sources and forward all those messages to the System Monitor Syslog receiver.


>Where is it used ?

This kind of device is quite common in network areas that require limited firewall forwarding rules. Such as DMZs or other secure networks, where forwarding from a single device is preferable, over having many devices forwarding out of the secure network to a single receiver on the far side of the network.


>How does it work?

The Syslog Relay Host configuration will strip the IP address from the Syslog message. This will reveal the actual device that sent the log message to the Relay Host, thus allowing each individual Log Source, even Log Sources of different types, to be identified by LogRhythm as the host of origin.



