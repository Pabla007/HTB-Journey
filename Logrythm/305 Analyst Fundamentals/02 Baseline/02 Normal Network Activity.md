
```
It is crucial to understand what "normal" network activity looks like in your environment. This helps you set a baseline, and recognize anomalous activity.
```

## Find Log Sources

Knowing your environment's log sources helps you learn to anticipate certain logs, and certain log activity.  

**A quick and easy way to view the log sources that are set up is from Search.**

1. Press the "**Search**..." button in the upper-right corner of the Web Console screen
2. Press the "**Log Source Filter**..." button on the top of the Search window to view all the log sources that LogRhythm is ingesting and filter them based on their metadata.
3. To complete the Log Source Filter step in the search process, simply add any log sources by pressing the "+" button and then OK when you're done. Then click search.


## **Filter Log Sources**

The Log Source Filter panel within Search gives us some useful information about our log sources.

## Prefer to see Dana's steps as a list? Click here!

**1) Name**
The log source or list name.  

**2) Entity  
**An entity is a logical grouping of hosts or networks (like a Security/Distribution Group in Active Directory, or a Contact Group in Outlook).  
  
**3) Log Source Host**  
The end point that the logs are originating from.  
  
**4) Log Source Type**   
The type or classification of logs that are coming in (like Microsoft Windows Event Logs). It's used to help LogRhythm process logs more efficiently because the software has built-in rules that apply based on log type



## **Dashboards (Overview)**

Knowing your environment also involves being familiar with the Web Console's three dashboards.

The **IT Operations Dashboard** includes events labeled as "Operations."

The ****Security Analyst Dashboard**** includes events labeled as "Security" or "Audit."

Unlike the prior two dashboards, the **Executive Dashboard** is unfiltered and includes all event data.

![[Pasted image 20240616170349.png]]



>[! bug] Dana's Advice

**Beware of Collecting Too Much**

## Determine Log Values

Not every log or log source is of equal value.

## Avoid Overload

If you don't think about what you're collecting, you'll end up collecting everything. And collecting everything is a quick path to overload.

## Collect Only What You Want

Ask yourself: "Will these collected logs be helpful and provide value?"

Think Comprehensively
Log Practice is about relevance and being comprehensive. Ask yourself, "What do I need to collect to get full visibility on a problem?

Understand The Pathway
The process starts by familiarizing yourself with your environment, but it continues throughout all phases of the TLM framework.

Consider This Log Recommendation Example
"I want to start/continue collecting X log because it has X data. And that data will help me detect X threat.”

Use Reporting to get the "Big Picture"
Reports can give you a 10,000 foot view by showing you a large amount of data over a longer span of time, such as 30 or 90 days.


**To learn more about Dashboards and customizing Widgets, visit** [**docs.logrhythm.com/docs/enterprise/web-console-user-guide**(opens in a new tab)](https://docs.logrhythm.com/docs/enterprise/web-console-user-guide) **and search "Dashboards" and "Widgets"**


