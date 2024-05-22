
## Read each question and make a guess. Then click to see the answer.


## What are the two object types that Entities contain?

1. Network records: define segments of your infrastructure that match how your IT department has defined the IP topology (the method and layout of IP addresses) for your organization.
2. Host records: define each known host within your organization. Host records allow for pinpoint accuracy in the weighted importance of log information that comes from that host’s Log Sources.


## What does the Entity Reorganization Wizard do?

The Entities Reorganization Wizard provides a method to migrate Host and Network records to new Entities. This wizard enables restructuring of the Entities to match changes in your network topology, system placement, or logical arrangement of assets.


# Key Takeaways

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

>[! Bug] I think this question can come

Silent Log Message Source Detection allows for the generation of a warning or error by a log source if it does not generate a log within an expected time frame.

<hr>

