
The Knowledge Base (KB) contains many options that can be enabled and configured to meet the needs of your organization.

![[Pasted image 20240531111526.png]]

**The Knowledge Base (KB) consists of a LogRhythm Required Objects Module and many other individual KB Modules.** 

- The LogRhythm Required Objects Module should be configured for all deployments. Then, additional individual KB Modules can be **e****nabled and configured to meet your organization's needs.**
- **E****ach KB Module has a single theme or purpose;** KB modules are often used in the following scenarios:
    - **Compliance Modules:** GLBA, PCI, GDPR, NERC-CIP, etc.
    - **Operations Modules:** LogRhythm Diagnostics
    - **Security Modules:** Threat Intelligence Service
- KB Modules and their associated objects are imported with a LogRhythm Knowledge Base (KB). 
- **T****he Knowledge Base Manager is the tool you'll use to manage the Knowledge Base Modules and their associated objects.** Here you can update the current Knowledge Base Modules, configure automatic update options, and check for recent updates.



**The Knowledge Base Manager cannot be opened while other Manager windows are open** (e.g. Deployment Manager or List Manager). If you encounter an issue while opening the Knowledge Base Manager, or if the option to open is grayed out, close all other windows within the Client Console and try opening it again.


**Reaching** [**kb.logrhythm.com**(opens in a new tab)](https://kb.logrhythm.com/) **requires that the Platform Manager be able to perform certificate lookups. If access is locked to just** **kb.logrhythm.com****, then the Root and intermediary certs can be installed on the Platform Manager to alleviate this issue.**


## **Access & Updates**

KB Modules are frequently updated to address changes in the threat landscape and regulatory frameworks.**** You can opt to have the updates downloaded and installed automatically ([kb.logrhythm.com(opens in a new tab)](https://www.kb.logrhythm.com/)) or import them manually. 

With the exception of the LogRhythm Required Objects Module, which is required for all LogRhythm deployments, you need only to enable the specific KB Modules that are relevant to your organization.


![[Pasted image 20240531112300.png]]


The Knowledge Base Manager is **accessed** from the Tools > Knowledge > Knowledge Base Manager menu.


**Knowledge-Based Objects**

The **building blocks of KB Modules are KB Objects**. 

KB Objects consist of the following:

- AI Engine Rules
- Alarm Rules
- FIM Policies
- GLPRs
- Investigations
- Lists
- Reports
- Report Packages
- Report Templates
- Tails
- Log Source Virtualization Templates


**KB objects can be used as either primary or dependent objects:**

**A primary object** is directly associated with a KB Module.

For example, a KB Module might include an Alarm Rule that utilizes a particular list. In this case, the Alarm Rule is a primary object, and the List is a dependent object.

**A dependent object** is associated with a primary object within a KB Module.


