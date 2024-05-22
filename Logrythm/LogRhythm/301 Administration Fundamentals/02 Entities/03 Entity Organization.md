
```
Entity organization involves grouping assets within a LogRhythm environment into structured segments that coincide with permission requirements for LogRhythm Administrators and Analysts. 
```
  

Entities are organized using a parent/child relationship.

**They go from top to bottom: Global > Parent > Child.**

Parent Entities (also called Root Entities) are listed below a Global Entity. Top-level Root Nodes (Parent Entities) can contain any number of Child Nodes below it. 

>[! bug] Note: Currently you can only place one level of Child Entities beneath a Root. You cannot have a Child Entity beneath another Child Entity.

In other words, as hosts and log sources begin to accumulate within an environment, it is often necessary to allow or restrict access to these objects by User Profile permissions, or simply organize assets in a way that makes sense from an administrative standpoint.


## Example

As an example, if an environment has one central office with several branch or satellite offices, an Entity structure that aligns with these offices can be constructed. 

Similarly, if an environment has multiple departments (as most do), an Entity structure can be designed to reflect this.

See below for additional examples:
![[Pasted image 20240516114842.png]]

Based on the layout of an organization’s environment, the following are examples of Entity design options:

- Geographic Location: An Entity may be structured with a company name as a Root Entity and office locations as Child Entities.
- Department: An Entity may be structured with a company name as a Root Entity and the various departments as Child Entities. (This can work well for smaller companies that have a single location).
- Function: An Entity may be structured with a company name as a Root Entity and terms such as Firewalls or VLANs as Child Entities.



## Benefits of Entity Organization

Entity organization accomplishes several things:

**User Permissions and Access**

Once an Entity structure has been established, user accounts with access to LogRhythm can be assigned granular permissions to perform configurations or view data only within their assigned Entities. For example, if an analyst is only supposed to have access to data from their specific office or site, permissions based on Entity structure can accomplish this.


**Host and Network Resolution**

As logs are delivered to LogRhythm, certain derived values are populated within metadata fields of indexed logs. As described in a previous module, metadata fields such as Known Host (Origin) and Network (Origin) are not populated by information within the log message itself, but are instead populated based on Entities and the objects within them – Host records and Network records, to be covered later in this module.

Entities, Host Records, and Network Records also directly affect other derived metadata, such as directionality and zone.

Without effective Entity organization, the Message Processing Engine (or MPE) is less likely to enrich valuable metadata within indexed logs. Because of this, it is important to develop a plan for an Entity structure, verify user permissions, examine logs for correct metadata, and return to the Entity structure for adjustments or improvements.
  
Note: The _Entities_ section within **LogRhythm Docs** provides additional detail in how the Message Processing Engine (MPE) performs host and network resolution within LogRhythm.


## Single Root vs. Multiple Root Setups

Entity structures are not limited to single-Root multiple-Child setups – multiple Root Entity setups are an option. However, these setups are reserved for environments with potentially overlapping IP address spaces, such as MSSP environments, or environments where identical IP addresses may be used from site to site.

The drawback to using multiple Root Entities in an environment that does not require one is that this may result in unresolved hosts and networks, due to the linear nature of resolution steps performed by the MPE. Root Entities act as a boundary for host and network resolution. In other words, as a log is processed, the MPE will determine Entity (Origin) or (Impacted) based on the Root or Child Entity that a log source belongs to. It does not look across multiple Root Entities.  

Note: If your company or organization is not an MSSP or does not use identical IP addressing for different sites, **it is recommended to build an Entity structure using a one-Root, multiple-Child setup**.


For more information on these topics, refer to the Entities section of LogRhythm’s Online Help: https://docs.logrhythm.com


>[! bug] Setting up entities correctly, and updating them as needed, is critical.

If entities are not set up well, **things may be missed, or you might waste a ton of time investigating a problem in the wrong place**, e.g. a problem may look like it originated in Payroll, when really the issue was in Sales.  
  
This is because **all derived metadata about location comes from entities**. LogRhythm assigns directionality (internal, external, DMZ) based on how the entities are set up.


>[! Question] Remember **Quantitative** and **Contextualized** metadata comes directly from log sources. **Derived** metadata is parsed out of how you build your entity structure.

