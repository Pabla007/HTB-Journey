
```
Remote collection configurations will vary, depending on the log source type that is being collected:
```


## Windows Event Logs

As discussed, using a service account with appropriate permissions, will allow a System Monitor Agent installed on Windows to communicate and pull logs from another Windows host. Generally, an agent will be configured to collect Event Viewer logs, but it can also collect logs from specified directories within Windows (flat files).

![[Pasted image 20240515114934.png | 400]]


## **Syslog**

- For a System Monitor to collect logs from devices, servers, and applications via the Syslog mechanism, the Enable Syslog Server setting must be selected.
- You have to specify the IP address, or the Network Interface card in the advanced properties of the Agent, especially if you have more than one network card in the LogRhythm Agent server. On some machines, like web servers, they may have dozens of IP addresses, so you need to record that too. 
- Syslog messages are transmitted via the network, typically over UDP port 514 (although both UDP and TCP Syslog servers are supported). In some cases, the default Syslog port is not used within an environment.
- LogRhythm supports custom Syslog ports, and the Syslog Server can be set to listen on any custom TCP or UDP port. Keep in mind that the System Monitor can listen on only one TCP and UDP port pair at a time. Keep in mind that you'll need to accept anything coming in over Syslog.

![[Pasted image 20240515122205.png | 400]]



