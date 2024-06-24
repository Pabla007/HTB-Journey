
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



