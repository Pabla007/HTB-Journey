
It is crucial to understand ideal placement for Agents and their required configurations.

Pictured below are some of the suggested locations and the reasons why you might install an Agent. When considering agent placement, you need to take into consideration your network architecture and consider whether Agents should be installed per VLAN or per data center, etc., as well as considering other options.

Most things can be collected from a central Agent that reaches out and grabs data remotely, but there are a few exceptions. For example: syslog over a stream is different than a Syslog File that is local (in which case you need a local agent - this includes Linux).

![[Pasted image 20240514131156.png]]
Note: Sources such as DNS Debug are very high volume log sources, so they really require an Agent on the machine.

