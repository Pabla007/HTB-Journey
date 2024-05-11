
```
A single, routine log may not be an issue. But context may make that same log more important, and become an event. Event Correlation is how the SIEM adds context.
```


> Key Terms in this lesson:
- **Event Correlation**
- **Detection**

## **What is an event?**

An event is just a more important log or collection of logs. A SOC Engineer can set up the rules that indicate some impact to the environment, like threat activity or system failure.


## **How does a SIEM identify an event?**

A SIEM can identify an event from a single log or a collection of logs and context.


>A single log
- For example, a single "Malware Not Cleaned" message is something that requires action and is therefore classified as an event.


>A chain of logs

Some logs aren't concerning on their own, but together may indicate suspicious activity. Take the following logs, for example:

- An account is created.
- An account is added to high level security group.
- An account logs into a secure server.
- An account copies data from the secure server.

Each of these logs may happen individually in an environment without causing concern. However, if they happen in this order within a certain amount of time, these actions could be tied to malicious activity. The SIEM can correlate these logs and generate an alarm.


>A single log plus context

Sometimes a single log message becomes an event because of its timing. For example, a message stating that a server has been patched isn't alarming if this is a known patch window. But, if a server patch is occurring outside a normal change control patch window, it could be the result of an attacker breaching a system based on a known vulnerability, and then patching it to prevent anyone else from using that known vulnerability (attackers don't like to share compromised systems). The patch + abnormal timing = an event that requires investigation.


## **What does Event Correlation look like in a SIEM?**

**Event Correlation** comes into play when a single log on its own is not classified as an event. Correlating two or more log messages, or adding context to a single log, means adding information to determine importance.


## **Detection & Event Correlation**

This is the stage where something of interest is **detected** by the SIEM. **Event Correlation** is the flagging of important logs as events, once detected. An event is simply a more important log that may require action. A single log or a sequence of logs can be correlated to indicate required action.

![[Pasted image 20240511160431.png]]

```
Malware not cleaned is the only log that, on its own, would require immediate action and would therefore be classified as an event. The other options may be correlated, then classified as events.
```

To learn more about LogRhythm's Data Normalization tools, visit [https://docs.logrhythm.com/lrsiem(opens in a new tab)](https://docs.logrhythm.com/lrsiem/) and search **AI Engine** or **AI Engine rules.**

