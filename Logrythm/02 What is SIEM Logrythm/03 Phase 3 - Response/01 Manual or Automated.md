
```
Human response doesn't always involve the SIEM, but most organizations will leverage a single system.
```


> Key Term in this lesson:
- **Manual SIEM Response**
- **Automated SIEM Response**


## **What is a SIEM Response?**

An Analyst can pre-configure a SIEM **Response** to make necessary changes to the environment or improves SIEM detection rules. Configuration and ongoing maintenance of SIEM detection rules cuts down on analyst fatigue.

![[Pasted image 20240512143131.png]]



**We will discuss 2 types of SIEM Response in this lesson:**


>Manual SIEM Response

A manual SIEM Response requires human interaction with the SIEM. With manual response, the person responding doesn't need direct access to the infrastructure to action necessary change.

- When to use: Manual SIEM action is required, or a response is preconfigured and needs manual approval to be actioned.
- Example scenario: Disabling an account after suspicious activity by remotely running a PowerShell script.


>Automated SIEM Response

An automated SIEM Response is pre-configured and can run automatically without approval.

- When to use: Alarms that have a 100% certainty that action will not have any ill effect on regular business functions.
- Example scenario: Quarantining an endpoint (isolating it from the rest of the network while keeping it running to avoid losing valuable data) or adding a suspicious user or external IP address to a user watch list.


## **Response: Manual or Automated?**

Using a SIEM for **Response** allows an Analyst to pre-configure common Responses and access infrastructure to make changes or update detection rules.


![[Pasted image 20240512174000.png]]


To learn more about LogRhythm's Response tools, visit [docs.logrhythm.com/lrsiem(opens in a new tab)](https://docs.logrhythm.com/lrsiem/) and search **SmartResponse.**

