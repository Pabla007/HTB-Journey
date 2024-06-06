
### What is a Use Case?

A use case is a set of actions or steps that define the interactions between an **actor**, a **system**, or a **device** in order to achieve a particular objective.


- A use case **defines the flow of data**—and the events within that flow of data—that need to be observed for the adverse conditions to be triggered as an event or alarm.
    
- The use case should define **who is to be notified** of this event and **how they should** **respond**.
    
- An **automated response** or action should be defined. If not automated, available responses that offer some form of automation based on approval mechanisms should be included, such as a LogRhythm SmartResponse.


A use case doesn’t have to be complicated; it just has to provide enough information for anyone to understand what was trying to be achieved.




Brute Force:   
**Password Guessing**

- Brute Force Attack against a SQL Server
- Targeting MS SQL "sa" account to gain access or execute commands internally in my network. 
- Learn more about the [**MITRE ATT&CK technique, Brute Force: Password Guessing**](https://attack.mitre.org/techniques/T1110/001/)




User Execution:  
**Malicious File**

- Attacks using PDF, XLS, EXE, or other to gain access. 
- The goal being to target the machine through execution of malicious code. 
- Learn more about the [**MITRE ATT&CK technique, User Execution: Malicious File**](https://attack.mitre.org/techniques/T1110/001/)


## Model 1 : Crown Jewel Analysis (CJA)

![[Pasted image 20240606172452.png]]

Crown Jewel Analysis (also known as Mission-Based Critical IT Asset Identification) is a process for identifying those cyber **assets that are most critical** to the accomplishment of an organization's mission.



## Model 2 : Attack Trees

![[Pasted image 20240606172837.png]]

Attack trees are conceptual diagrams showing an asset or a target that might be attacked and the **various methods or techniques** to do this.


## Model 3 : Mind Maps

![[Pasted image 20240606173033.png]]

Mind maps represent the attack **radiating connections** from the center.


# Model 4 : Pyramid of Pain

![[Pasted image 20240606173120.png]]

The Pyramid of Pain model represents the **degree of difficulty for the adversary** if the Analyst can respond to the several types of indicators at distinct levels within the pyramid. 

It is complimentary to the Cyber Kill Chain at every phase.



**Example Use Case Template**

It is essential that use cases **contain all the relevant points** so that any member of the IT Security Team can pick up the document and understand what is trying to be achieved.



## An example of a use case template

| **Name**                      | A concise and descriptive scenario                                                                                                     |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Purpose**                   | Use case goal – what is to be achieved?                                                                                                |
| **Problem**                   | A description of the problem to be solved                                                                                              |
| **Requirements**              | What actions should the SOC team or Analyst undertake? Actions should be achievable with an option for automation as needed.           |
| **Design**                    | What are the objectives? Follow SMART methodology: specific, measurable, attainable, realistic and time-related goals.                 |
| **SOC Notifications**         | Who and how will people be notified (e.g., dashboards or alarm emails)?                                                                |
| **Use Case Data Source(s)**   | What data sources will be needed? Align to MITRE ATT&CK, cyber kill chain, or other methodology.                                       |
| **Assumptions & Limitations** | As an example, if this use case requires LDAP, then the assumption is that all new LDAP servers will be configured to log to the SIEM. |


## An example from LogRhythm’s Threat Module

View an example of **LogRhythm’s Threat Module** information and how the information above is included. 

Note that LogRhythm’s Threat Module information is more generic, as details regarding environment specifics, infrastructure, or logging capabilities would not be available to LogRhythm initially.


![[Pasted image 20240606173426.png]]


## Where to find the Knowledge Base

To access the Knowledge Base, open Tools > Knowledge > Knowledge Base Manager. 

**Note: if any other windows are open, the KB will not be available to open.**


