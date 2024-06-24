
```
What activity triggered the alarm? How did it affect our network? Drill into Alarm data to view details.
```

Quick reminder: when an AI Engine rule is triggered as true:

- The AI Engine generates a new event that is sent to the Platform Manager. 
- It may also be set to trigger an alarm (that's what we saw on the Alarms page; an AI Engine rule was triggered as true when it was comparing metadata from logs being ingested).  

Let's drill into the Alarm card to see the log data that triggered this rule as true.


## Alarm Drilldown

1. **Click the Drilldown icon** on the upper-right side of the Alarm card. This will perform a drilldown and pull back the log data that triggered this rule as true.
2. **Then,** **click the "Completed: All Results" link** in the taskbar once the search results have fully loaded. 
3. **This will open the Analyze page.** 


## Prefer to see Dana's steps as a list? Click below!


## Top Classification & Top Common Event

**1) Top Classification**  
The **T****op Classification** is Network Deny. This makes sense based on the alarm details we've seen.  
  
**2) Top Common Event**

The Top Common Event is Traffic Denied by Network Firewall (it is cut off, so I have to hover over the name with my cursor to expand it out in full). Again, this makes sense based on the alarm details we've seen.


## Node-Link Graphic

**3) Node-Link Graphic**

The Node-Link Graphic widget allows you to visualize relationships, patterns, and abnormalities present in log data. 

These relationships include, but are not limited to, network traffic between a source and destination host, and authentication between an origin user and a destination host. 

**Hover over nodes** to see additional data (play video - click the icon on the far right of the player to view in full screen). We can see adam.hall and the network deny traffic from his computer. 

Note: classification colors and widget filters, etc, are defined in the widget criteria (if you wish to know these details, click the cog icon on the widget to view the widget inspector pane, which is distinct from our typical log message Inspector panel).



## Top Host (Impacted) & Top Host (Origin)


**4) Top Host (Impacted)**

The Top Host Impacted looks like an external IP address; it's probably not in my entity structure, so it's somewhere outside.  
  
Again, this lines up with what I saw earlier in the Inspector panel.

**5) Top Host (Origin)**

Host (Origin) is where the connection or authentication came from (i.e. the host that initiated the connection).

  

In this case, the Host (Origin) lists a named host. Again, this is in my entity structure because it has a name. Remember, the Inspector panel made us think it might be Adam Hall, since he was listed as the User (Origin).

## Top Application & Top Direction & Top Process Name

**6) Top Application**

It's going to the global entity. It's HTTPS, that's normal. That's what almost all internet traffic is.

  
**7) Top Direction**

LogRhythm works out direction by using information from the location of the originating host and its destination. An internal host going to the internet would be outbound, as in this example.


**8) Top Process Name**

Like everything else, this is still normal. I'm not seeing any problems here, other than the firewall denying it.


Right now this is almost looking like a false positive to me, or at least it's not immediately clear why I should care... but I should continue to qualify to make sure.


## **Now we know what this alarm is telling us**

1. The log message that triggered this rule as true says: firewall denied an outbound connection to Dropbox from Adam Hall's computer.

2. Through this, I've identified a security breach and a potential Administrator fix since the url in the log message was not parsed out.

3. Before moving to our next Qualification step, let's add this log to our case.

![[Pasted image 20240624144537.png]]

![[Pasted image 20240624144608.png]]


## Self-Reflection Questions

I am always asking myself: 

- Are there ways to speed up information retrieval?
- Could I have implemented a SmartResponse or Contextualized Action to speed up my Mean Time To Detect?

## Parsing Matters

The URL not being in the event field could create problems: it means I can't use the URL to create a custom dashboard, specialized widget, custom list, AI Engine rule for every time someone goes to Dropbox, or run a search via URL.


## Communicate Parsing Issues

I would definitely contact my LogRhythm Administrator, Support team, Professional Services, or Co-Pilot team in this situation. I could tell them that it didn't parse out the URL the way I expected it to and that we need to fix it.


Sometimes there is other data in our log messages that we might find useful when evaluating data and rather than have to search the raw log message for this data, we may be able to improve our speed of investigation by improving the log parsing rules, to show the URL in one of the metadata fields. For example, I would like to have seen this URL even earlier, when we were looking at the AIE Rule Block Summary in the Inspector panel, prior to our Drilldown.

