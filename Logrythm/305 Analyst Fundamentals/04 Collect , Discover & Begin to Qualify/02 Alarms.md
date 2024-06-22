
## Alarms: a helpful discovery tool


>WHERE DO ALARMS COME FROM

The LogRhythm platform includes a real-time alarming system that can notify users when certain criteria are met. 


>HOW DO THEY WORK

Alarms announce the presence of log activity using created or existing **Alarm Rules** and can be configured to detect operational or security-related events or logs. 


>ANALYST'S ROLE

Based on log activity or criteria being met, an alarm can trigger and either generate a viewable alarm within the console or a notification that is sent to designated recipients, or both.


<hr>

WHERE DO ALARMS COME FROM

The LogRhythm platform includes a real-time alarming system that can notify users when certain criteria are met. 

Alarms announce the presence of log activity using created or existing **Alarm Rules** and can be configured to detect operational or security-related events or logs. 

Based on log activity or criteria being met, an alarm can trigger and either generate a viewable alarm within the console or a notification that is sent to designated recipients, or both.


<hr>


HOW DO THEY WORK
- Administrators set up alarms. 
- They are triggered by rules or thresholds which are built on metadata filters and log source criteria.
- There are 2 ways to create an alarm: From Alarm Rules or Advanced Intelligence (AI) Engine Rules.
- Alarm Rules: These alarms are triggered by a single event or log and are only used for operational/health monitoring.
- AI Engine Rules: These alarms are triggered by complex activity involving multiple logs – these are for threat detection and are the recommended method of rule creation.
- RISK colors: gray/white: lowest risk,  orange: medium risk, or red: most serious risk.


<hr>


ANALYST'S ROLE
Though administrators create rules, administrators and analysts collaborate to test, tune, and enhance the rules.

Analysts help administrators by communicating:
- What they want to be collected.
- What criteria should trigger an alarm.
- Whether rules are triggering correctly.
- Whether the AI Engine is generating too many alarms.


Though administrators create rules, administrators and analysts collaborate to test, tune, and enhance the rules.

## User Profiles: Why does my dashboard look different?

Note: you may notice differences between my Web Console and yours. 

That's because we may have different user profile permissions, set up.

However, as a Tier 1 SOC analyst, this is what you would see...



## Prefer to see Dana's steps as a list? Click here!

**1) Alarms Page**

- Navigate to the Alarms page by clicking the Alarms tab.

**2) Priority Level**

- Out of all these alarms, I notice that a high-risk alarm went off. This alarm has a Risk-Based Priority score of 51. 
- A lot of alarms over 20 will be considered high risk. This is significantly over 20, or even 30 which is the higher threshold.
- So this 51 is important and definitely worth looking into. We want to prioritize it.

 3) **Alarm Card** **Title**

- The title is also interesting: "Cloud File Sharing Blocked." Hmm. Based on this title, I assume that someone was trying to share a file on some site that isn't authorized for file sharing.

<hr>

## KEEP QUESTIONING
To be a good Analyst, it's important to keep questioning. I'm always wondering: why did that change? Why couldn't I see that? What caused me to stop seeing that?

- **I'm constantly questioning the status quo** by asking who, what, where, why, and how questions.


## CONFIGURE ALARMS/ALARM FATIGUE
Alarm fatigue is real. You could have too many alarms, or have too few alarms. 
**Communicate with your Administrator to optimize your alarms.**


## SEE PAST ALARMS
Alarms are configured based on known threat behavior. **Relying solely on alarms can give you a sense of false security;** Zero Day Vulnerabilities may rely on previously unknown techniques.  
  
In addition to alarms, **use the visual tools in LogRhythm's web console to alert you to suspicious or unusual activity.**


