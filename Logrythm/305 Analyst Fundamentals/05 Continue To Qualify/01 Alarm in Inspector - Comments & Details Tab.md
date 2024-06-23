
**Alarm cards only tell you so much. Use the Inspector panel to qualify alarms.**

![[Pasted image 20240623211004.png]]

## **Inspector Panel - What Happened?**

**Want a challenge?** Try interpreting the information on the screen below **before** clicking through Dana's explanation. See how closely your findings match Dana's.


## **Prefer to see Dana's steps as a list? Click below!**

## Open the Inspector Panel


**1) Data, Comments & Details Tab**

- **C****lick** on the alarm to open the Inspector panel's **Data Comments & Details** tab.
    - Or press "I" to open the Inspector panel. 
- This way, we can see more about the rule and determine whether this is a false positive or something we need to look into.


## Inspector Panel: Data, Comments & Details - Event Data


**2) Suspicious Classification**

- The Classification is "Suspicious."
    
    "Suspicious" is part of the Security Events category. It immediately tells me:
    
    - This is a security event. 
    - Something is occurring that is not normal in my environment, which means I should look into it.

**3) Zone**  

- The Zone (Origin) is Internal.
- This tells me where the traffic originated from.
    - In LogRhythm we have three zones: internal, external, and DMZ.
    - Zones are important data points for:
        - Understanding context and direction (what is talking to what).
        - Determining what is normal or suspicious.

**4) Entity**

- The Entity (Origin) is our finance team. 
    - LogRhythm uses entities to logically group objects such as networks or endpoints.
- This tells me that an internal endpoint in the finance entity was involved in this alarm. 
- Since our alarm involves finance, it seems especially important to me.


## Inspector Panel: Data, Comments & Details - AIE Rule Block Summary

**5) Rule Block Summary: Host List (Origin) & User (Origin)**

- The Rule Block Summary gives us information about the alarm's origin.
- We know the **Host List (Origin)** is an internal device because it is a named host and has a star against its name, meaning it is known to LogRhythm. 
- We also see that the **User (Origin)** is Adam Hall. Since we already saw that it was internal and from finance, we can assume this PC belongs to Adam Hall, who is a member of our Telectric Finance Team.

**6) Rule Block Summary: Host List (Impacted)**

- Hmm, interesting. The **Host List (Impacted)** must be an external host because I don't know what it is.
- This is worth looking into because:
    - It is the only detail here I can't immediately identify.
    - It is a piece of unique information, specific to this scenario, that I can leverage to further qualify this situation.
- So I take note of that: what is this impacted host?


## Scenario End

Let's dig into this Alarm's construction in the Inspector window by:

1. scrolling down to look at the Alarm Details, and then by
2. looking at the AI Engine rule tab itself

## ****Inspector Panel - Why Was this Alarm Constructed?**** 

Let's look at the alarm's configuration and purpose, so we can understand why it even qualified as an alarm in the first place.


## Prefer to see Dana's steps as a list? Click below!

## Inspector Panel - Continued

**1) Scroll**

Scroll down in the Inspector window to the bottom "Details" section.


**2) Alarm Description**

The Alarm Description tells me: "An attempt to access a Cloud Sharing Service by a user who is not approved to use such services. Exception for Microsoft One Drive."


**3) Additional Details**

The Additional Details tells me: "Cloud Sharing Services that are currently configured to be blocked are: IDrive, SugarSync, and DropBox. An exception to this rule is Microsoft OneDrive."  
  

Oh right. Now I remember this rule!

- We were worried about data exfiltration because it happened at another company in town.
- We started working with LogRhythm's Analytic Co-Pilot team, and they helped us create a Cloud File Sharing alarm right away.

(For more information about LogRhythm Analytic Co-Pilot services, see "Dana's Advice" at the end of this lesson).

