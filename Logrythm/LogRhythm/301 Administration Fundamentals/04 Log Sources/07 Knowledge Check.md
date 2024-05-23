
## What do Log Sources Represent?

Log Sources represent the individual log files, log feeds (such as Syslog, NetFlow, or SNMP), and data feeds collected by LogRhythm. Log Sources are associated with Host records in the Entity structure.


<hr>


## Key Takeaways


Entities are the organizational apparatus within LogRhythm for Host Records and Network Records, allowing for controlled access to LogRhythm objects throughout the platform.


<hr>


Host Records represent Known systems (or Known Hosts) within an environment. Network Records represent ranges of Known IP addresses (or Known Networks) within an environment. Both have settings for Risk and Threat levels.

<hr>


The log source onboarding process can take various forms using a System Monitor Agent or Open Collector: local collection, remote collection, or log forwarding.

Flat Files and Windows Events can be collected either locally or remotely. UDLA and Endpoint Monitoring logs are reserved for local-only collection. API log collection is reserved for remote collection by an Agent or an Open Collector. Collection of centralized Syslog, SNMP Traps, and forwarded Windows Events can be accomplished through log forwarding.


<hr>


All log sources require that a Log Source Type and a Log Processing Policy be selected.

Depending on the log source (e.g. Flat File, API), certain configuration fields will be required related to that log source (e.g. a Flat File Path and a Date Parsing Format).


<hr>


Silent Log Message Source Detection allows for the generation of a warning or error by a log source if it does not generate a log within an expected time frame.


<hr>


