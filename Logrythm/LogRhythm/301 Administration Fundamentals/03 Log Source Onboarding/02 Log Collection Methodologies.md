
## Three primary methods can be used to collect logs:

> Local Collection by a LogRhythm System Monitor 
> **For this, an agent is installed locally on the endpoint. With the introduction of Open Collector, the use of beats on various endpoints can be used to send local log data to the Open Collector instance for processing. This includes:

    - Flat File, i.e. Windows IIS logs or Apache Logs on Linux
    - Windows Event Logs (security, application, PowerShell)
    - Universal Database Log Adapter (UDLA) (oracle and McAfee EPO)
    - Endpoint Monitoring via built in System Monitor Agent Features


> **Remote Collection by a LogRhythm System Monitor or by Open Collector**  
    Flat File, Windows Event Logs, UDLA (Database log collection), and API collection can all be performed remotely.


> Log Forwarding  
    **Centralized Syslog allows various endpoints to send their logs via syslog to a centralized syslog server that then forwards this to a LogRhythm System Monitor Agent.  


In other words, Log Forwarding allows for the centralized collection on a dedicated log collection server. Logs are then collected from this central point for processing. This includes:
    - Centralized Syslog (secure or non-secure) via UDP/TCP
    - SNMP Traps 
    - Windows Event Forwarding


