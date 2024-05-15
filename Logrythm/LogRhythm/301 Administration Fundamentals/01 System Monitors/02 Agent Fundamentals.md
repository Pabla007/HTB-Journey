
```
Agents provide log data collection across various operation systems. This can be done locally, remotely, or via Endpoint Monitoring. Licensing options should also be considered.
```


>Windows or *NIX Environments
- Agents provide log data collection across various operating systems. They can be installed on **Windows** and ***NIX** platforms, in both 32-bit and 64-bit configurations.


>Local vs. Remote Collection-
- Logs can be collected **locally** (where an Agent is installed), or from **remote** devices. 
- When installed on a single machine, we can also use the **Endpoint monitoring** feature. 


>Licensing Options
- System Monitors are licensed in one of three ways: **Lite**, **Pro**, and **Collector**.


>Local vs. Remote Collection

## Local Collection

**Local Collection means an Agent is installed on a machine and pulls the logs from that same machine**.

System Monitors can collect from Flat Files and other Log Sources, metrics, and utilize Endpoint Monitoring features built into the System Monitor itself. This includes:

- File Integrity Monitoring
- Registry Integrity Monitoring
- Data Loss Defender
- Process Monitoring
- Network and User Activity
- Flat File, local Windows Logs


## Remote Collection

**Remote Collection means the Agent is installed on one machine, and it can reach out and grab logs from many other workstations and servers.**

Remotely, System Monitors may collect logs using several communication methods such as:

- Windows Event Remote Collection
- API-based log sources
- UDLA log sources (UDLA basically means databases, like Sequel, Oracle, DB2)
- Secure Syslog and Syslog (these can be received, not necessarily grabbing)
- Flow Data - such as NetFlow, sFlow, IPFIX, and J-Flow
- CheckPoint OPSEC or syslog
- SNMP Trap Collection (these tend to apply to companies with older technology)
- Flat File Log Collection

