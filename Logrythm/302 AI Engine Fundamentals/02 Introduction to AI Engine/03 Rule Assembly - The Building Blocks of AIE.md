
### **Construction of an AI Engine Rule involves the use of Rule Blocks, with every AI Engine Rule consisting of at least one block.** 

- Rule Blocks vary in function and, depending on what activity an AIE Rule is meant to detect, different rule block types will be used to capture specific log activity.
- Each AI Engine Rule Block type is in the left panel of the AI Engine Rule Wizard. Some blocks can be used alone, some must be used in combination with another block to create an AIE Rule.


### **LogRhythm supports four Rule Block types with each type consisting of specific Rule Blocks:**



## **Log**  
Looking for one, single log message in your environment

**Example:** Windows security event log

**Rule Block varieties:** 

- Observed
- Not Observed Compound
- Not Observed Scheduled



## **Threshold  
Looking for a pre-determined number of identical logs within a given period of time.

**Example:** 10 failed authentication attempts in 1 minute

**Rule Block varieties:** 
- Observed
- Not Observed Compound
- Not Observed Scheduled


## **Unique Values**
Looking for a pre-determined number of _nearly_ identical logs within a given period of time.

**Example:** 10 unique logins in 5 minutes  

**Rule Block varieties:** 

- Observed
- Not Observed Compound
- Not Observed Scheduled


## **Behavioral**
Can monitor for approved activity, perform statistical analysis, and observe trends.

_*Behavioral Rule blocks are very complex and will be covered in subsequent lessons_

**Rule Block varieties:** 

- Whitelist
- Statistical
- Trend


>[! bug] Behavioral Rule
>**The Behavioral Rule Block type is different from the others - it can be used to detect activity that is much more complex and consists of Whitelist, Statistical, and Trend Rule Blocks.**


## Observed Logs

Matching criteria were observed.

- Example: Windows Security Event Log was observed.
- Requirements: None


## Not Observed Compound

Something we were expecting to see after a given criteria, but we did not see it.

- Example: Backup success message expected after backup started.
- Requirements: Must follow another rule block, cannot have any rule blocks after them.


## Not Observed Scheduled

Something we were expecting to see within a certain timeframe, but it did not happen within that time.

- Example: Backup success message expected at 3 am.
- Requirements: Must be the only block in the rule.

>[! bug] **Log Observed, Unique Values, and Threshold Rule Blocks will only evaluate data for a maximum of 7 days.**


### **Rule Block Examples**

Watch the short video below for an overview and helpful examples of the nine varieties of rule block types within the three categories: Log, Threshold, and Unique Value – Behavioral Rules are more complex and will be covered in detail later.

![[Pasted image 20240606204214.png]]

Examples of all 9 varieties of the 3 basic rule types (Log, Threshold, and Unique Value)

### **Compound Rules:**

 Simple Alarm Rules vs. Rule Blocks

Simple traditional Alarm Rules are static and linear in nature. They are configured to monitor for specified criteria found in a single log message, or a number of these same logs occurring within a specified time span. 

Rule Blocks are what enable the AI Engine to evaluate and correlate multiple logs. The **AI Engine Rule Blocks can be combined with each other to make compound rules** capable of detecting sophisticated external attacks, internal threats, complex operational issues, and much more.

## Compound Rules

- A Compound Rule is an AIE rule using 2 or 3 rule blocks for complex data correlation (3 rule blocks is the maximum in any one AI Engine rule)
- Different types of Rule Blocks can be used in Compound Rules. As an example, a rule could utilize a Threshold Rule Block followed by a Log Observed Rule Block. 
- AIE Rules pass information from one block to the next to ensure correlation of specific data.

![[Pasted image 20240606204526.png]]

Create compound rules in the AIE Rule Block Designer

### **AI Engine: Visibility and Actions**

AIE is designed to create visibility and allow you to execute actions. 

- First, you want your Analysts to be able to recognize something abnormal quickly and AI Engine rules help by pointing out subtle differences and key indicators of abnormality.
- Then, when criteria for an AI Engine Rule is matched, LogRhythm can take any of the following actions, as specified in the rule:



## AIE forwards AIE Events to Event Database on PM

**The AI Engine will forward AIE Events to the Events database on the Platform Manager (PM).** These Events supplement the Risk Based Priority (RBP) Event identification performed by the Message Processing Engine (MPE) on the Data Processor.

- The PM forwards all AIE Events to the LogRhythm Consoles. AIE Events can be viewed in the Dashboards and found in searches and reports.
- The AI Engine Events are easy to differentiate from the Events identified by the MPE because they are preceded with AIE and the AI Engine Rule name.



## ARM service triggers AIE Alarm

**The ARM service on the Platform Manager will trigger an AIE Alarm.**

- AI Engine Rules can be configured to generate AIE Alarms based on a successful match of the criteria specified in the rule.
    - The PM forwards all AIE Alarms to the LogRhythm Consoles. AIE Alarms can be viewed in the Alarms page.
    - The AI Engine Alarms are easy to differentiate from the traditional Alarms in LogRhythm because they are preceded with AIE in the AI Engine Rule name.
- AI Engine Rules can be configured to notify a Person or Role of the AIE Alarm or AIE Event.


## Execute a Smartresponse action

**Execute a Smart Response action.**

- AI Engine Rules can be configured with a Smartresponse auto-remediation action.
- The ARM service on the Platform Manager is responsible for initiating SmartResponse actions. These actions can be configured to run automatically or upon approval.

![[Pasted image 20240607014212.png]]

As criteria for an AI Engine Rule are met, LogRhythm SIEM performs the following actions: AIE Events are made visible, AIE Alarms are made visible, Notifications are sent, SmartResponse remediation actions are performed.

### **Notification Types:**

The **ARM** or **Notification service** on the Platform Manager can send notifications in several ways. People and Roles, created in LogRhythm under the People tab of the Deployment Manager, may be assigned a contact method of SMTP.

Once the appropriate option is selected, AI Engine alarm notifications can be sent in HTML format which allow for easier reading and a greater detail of information. To send these enhanced notifications, select the HTML option in the Notification Policy Manager.


