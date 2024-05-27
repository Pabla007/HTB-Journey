

You can configure the Windows System Monitor Pro or Collector Agent to collect data from database tables, usually targeting tables that contain database audit or log data. LogRhythm stores the data from a table row, as a log, to allow analysis tools such as Investigator or Tail to review the information. Universal Database Log Adapter (UDLA) logs are treated as any other log types. They can be:

- Forwarded as events
- Associated with alarms
- and Archived

UDLA Log Sources must be configured with an **ODBC or OLE DB connection string**, **SQL Query** **Statement**, and **Output Format**. To help you with the configuration of the UDLA Settings, the LogRhythm Help Guide contains connection, query, and output format strings for supported UDLA Log Sources.


>[! bug ]
>
>**Only a System Monitor Pro or Collector Agent can collect UDLA Logs.** 

LogRhythm Agents do not come with Database Connection software. Therefore, as an example, if you wish to connect to an Oracle Database, you must install the tools from Oracle on the Agent’s host to do this.



![[Pasted image 20240528044818.png]]


**UDLA configuration guides are available in LogRhythm Docs. Make sure you are signed in to Docs, then** [**CLICK HERE**(opens in a new tab)](https://docs.logrhythm.com/devices/docs/udla-log-sources) **to access them.**


![[Pasted image 20240528044947.png]]



>UDLA TROUBLESHOOTING

The System Monitor Pro or Collector Agent requires that an OLE DB or ODBC driver be installed on the Agent host to connect to the specified Database Management System. A 64-bit System Monitor Agent is required.

ODBC/OLE DB drivers must be installed and configured prior to data collection. They are available from the website of each supported database vendor.

The Test feature requires that the appropriate ODBC or OLE DB driver be installed on the Client Console host.

An ODBC Connection string is only available on the configured host. If you move a log source to a different host and System Monitor Agent, you will need to recreate the ODBC Connection with the same Name on this new collection host.



>CLOUD COLLECTION STRATEGIES

PRINCIPLES OF CLOUD COLLECTION

**Cloud Local** – Cloud-based logging and reporting SaaS Services. Support for centralized logging for multiple subscriptions or tenants storing logs in one workspace.

**Cloud to Cloud** – Multi-Cloud, Operational Monitoring, and log collection is more complex in many multi-cloud scenarios. The log and reporting tools would use a hybrid approach to log collection.

**On Premise** – Hybrid network and directory synchronization allow existing log collection tools to act like cloud is a network extension (AWS Direct Connect). APIs and other exports used to pull logs from cloud native or other centralized solutions.

These are only some examples. There are other ways of connecting to cloud resources via site-to-site VPNs, etc. The type of service being used or consumed will depend on whether you can collect the logs and in what format they are available.



>PRINCIPLES OF CLOUD COLLECTION

Cloud log sources can be collected by a LogRhythm Agent, Open Collector, or via push to an On-Premise LogRhythm System Monitor Agent.

The picture below explains the requirements for collection of log sources from cloud sources.

![[Pasted image 20240528045643.png]]




![[Pasted image 20240528045417.png]]




