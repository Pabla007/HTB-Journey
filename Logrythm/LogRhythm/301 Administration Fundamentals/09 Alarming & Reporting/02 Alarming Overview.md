
The LogRhythm SIEM Platform includes a **real-time alarming system** that can notify users when certain criteria are met.


### **We'll explore these topics in more detail in this lesson:** 

 - [ ] Alarms can generate from both **Alarm Rules** and **AIE (Advanced Intelligence Engine) Rules**.

 - [ ] Alarm Rules are limited to triggering from **one instance of a log**. (Complex log activity is reserved for AIE Rules.) 

 - [ ] **Not every log is an Event**, but a log that precedes or follows a security event may constitute log activity that warrants an alarm or notification.

 - [ ] **Notifications** are available for delivery to recipients on the triggering of a rule.



### **The Structure of an Alarm Rule**

Alarm Rules are built on a series of metadata filters and log source criteria, with additional settings available for configuration. 

The properties of an Alarm Rule include a series of criteria and requirements captured in various tabs that, when met, trigger the alarm itself. Explore the tabs of an Alarm Rule in the graphic below to learn more about the specific functions of each:


![[Pasted image 20240529181603.png]]

## Primary Criteria

Primary Criteria specifies the primary set of metadata to be detected by a rule. For example, if any instance of Warning or Error Classifications are to generate an alarm, they can be specified with the Primary Criteria tab. Primary Criteria entries are not limited to one metadata field – multiple metadata fields and values can be specified.


## Include Filters

Include Filters allow additional metadata field specifications to be included in rule criteria and are generally used for values that may occasionally vary, perhaps as testing of the rule is conducted.


## Exclude Filters

Exclude Filters allow for omitting certain metadata field values among those that would otherwise meet rule criteria. For example, if every IP address within a subnet should be included in a rule with the exception of a small range, a fast way to prevent these addresses from triggering the rule and generating a false positive would be to specify them in the Exclude Filters tab.



## Day and Time Criteria

Day and Time Criteria allow for rules to be active only during scheduled times, such as during business hours.


## Log Source Criteria

Log Source Criteria provide a way to limit the processing of log data and activity to specific log sources, thereby significantly improving the efficiency of a rule.


## Aggregation

Aggregation allows for grouping occurrences of qualified activity that would trigger an alarm. If occurrences meet a specified number, only one alarm will be generated.


## Settings

The Settings tab provides options for Alarm Suppression, custom rule names for notifications, and Data Segregation by Entity as needed.


## Notify

The Notify tab allows for specifying recipients of alarm notifications as they occur.


## Actions

The Actions tab allows for assigning automated actions (or Smart Response actions) in the event of an alarm trigger. More than one Smart Response can be assigned.

## Information

The Information tab provides fields for the Alarm Rule name, the Alarm Group, descriptions of the Alarm Rule, and additional details.


### **Diagnostic Alarms**

Out-of-the-box alarm rules are available for detecting operational issues with LogRhythm-related components or processes. Flip the cards below to learn more about the logistics of diagnostic alarms.


## Out-of-the-Box Alarms
Most alarms within the Alarm Rules tab of the Client Console are available **out-of-the-box as part of Knowledge Base modules**.

They include LogRhythm-specific Diagnostic Alarms which trigger if LogRhythm-related components encounter an issue.


## Common Diagnostic Alarms
The LogRhythm Agent **Heartbeat Missed** alarm, which triggers if any active System Monitor Agent does not generate a heartbeat within its allotted time.

The LogRhythm **Silent Log Source Error** alarm, which triggers if any log source with Silent Log Message Source Detection enabled does not generate a last log message within the set time.


## Addressing Alarms

Most alarms, especially those dealing with the LogRhythm platform, will be **addressed by the LR team**. 

However, the two examples provided above may need to be **addressed from onsite**.


## Creating Alarm Rules
New Alarm Rules can be created in the **Alarm Rules tab**; however, due to their “one log” limitation, **it is recommended to use AIE Rules for custom alarms** (even when detecting one instance of a log only).

_We will cover AI Engine Rules in a later lesson._


