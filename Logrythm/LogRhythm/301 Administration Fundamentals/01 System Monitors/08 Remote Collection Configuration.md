
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



## Syslog Relays

**Syslog Relays**

Every System Monitor supports collection of Syslog data direct from devices, servers, and applications, or from a Syslog Relay, such as Syslog-NG or rSyslog device. 

The LogRhythm System Monitor requires that the Syslog Relay's IP address be provided, so that the individual Syslog messages can be identified correctly for each Syslog source. When the System Monitor sees an IP listed here, it uses special parsing to determine the true source of the log.

LogRhythm processes each log message individually. If a Syslog message is provided by a Syslog Relay, the Message Processing Engine (MPE) must be able to identify where each log message originated from. Using a router or firewall as an example, the MPE must be able to look past a router/firewall IP address and identify the hosts generating the traffic. If this differentiation did not occur, every log message would appear to originate from the router/firewall.

System Monitors can be configured to listen for Syslog messages on multiple network interface cards (NICs), allowing for versatility in deployments and a maximized collection from Syslog feeds.



## Flow Data

**Flow Data**  
NetFlow, sFlow, and J-Flow are network protocols that capture IP traffic information on a network, typically used to monitor network traffic and perform statistical analysis of network usage. These protocols are supported by many network devices, such as Juniper (J-Flow), Cisco (NetFlow), and others.

System Monitors can collect NetFlow, sFlow, and J-Flow data. To collect this information, a Pro licensed System Monitor's NetFlow, J-Flow, or sFlow Server must be enabled in the System Monitor Agent Properties window.  

Most Flow data will be collected and stored in the Archives only and will not be forwarded to the Platform Manager as Events, by default.

LogRhythm's Network Monitor can collect and provide Flow data to the LogRhythm Platform, although this data is not transmitted as Flow data. The Network Monitor repackages this data as Syslog and transmits that data across the normal Syslog channel.


## API Log Collection

For select log sources, a System Monitor Agent installed on Windows is capable of remotely collecting logs via API connection.

Log source specific .ini files are available in a _config_ folder within the installation directory of a System Monitor Agent and require information to be populated in these files specific to the log source connection. 

Once populated, the path to an .ini file is entered into a File Path field of the respective log source.

![[Pasted image 20240515144140.png | 400]]

## LogRhythm Documentation: API Log Collection

To assist with collection configurations for various API log sources, LogRhythm’s Online Documentation (https://docs.logrhythm.com/) contains a Device Configuration section that outlines required steps for many of these sources.


