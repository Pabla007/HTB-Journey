
**What are System Monitors used to collect?**
Local and Remote Log Data


**What does a System Monitor's configuration policy determine?**
Where and how the logs that it collects are processed.


## Takeaways

Depending on log source type, System Monitors can require local or remote collection configurations.

As examples, Flat Files over 10MB are required to be collected by a local agent, whereas API and Flow log sources can only be collected remotely.

<hr>

Agents can be onboarded by either Acceptance or Association.

Acceptance is reserved for Agent records not already present in an environment. Association is reserved for Agent records that existed prior and need to be restored.

<hr>

System Monitor Agents require a license type as part of the onboarding process. License types include Lite, Pro, and Collector.

The license type to be selected will depend on the log source types that an Agent is assigned to collect. License availability can be viewed in the License Report, accessible within the Help > About LogRhythm menu in the Client Console.

<hr>

System Monitor Agents should be configured for Least Privileged Access, which allows for improved security in remote collection of log data.

Examples of remote collection requirements under a Least Privileged configuration include full control of the installation directory path, read permissions to target directories or files, and membership in the Event Log Readers group in Active Directory.

<hr>


Configuring Agents for remote collection will require firewall rules for specific ports.

For example, syslog will require port 514, by default.


```
Service Account - LPE 
Syslog Relay - Message Processing Engine - router / firewall

User Activity Monitoring (UAM)
The Agent can see it before the operating system does!
```

