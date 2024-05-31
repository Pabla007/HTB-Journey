
Risked Based Priority (RBP) values will affect what Events are displayed in the Web Console.

## **Reduce the "Noise."**

Analysts will often have an overwhelming amount of data to review in the LogRhythm Console dashboards. Removing unnecessary Events from the Analyst's view helps to reduce the "noise." 

****The Risk Based Priority (RBP) scale helps control the volume of logs forwarded as Events to the Platform Manager.****

The Global Risk Based Priority (RBP) scale makes it possible for you to **filter out lower-risk Events from entering the Console, allowing for more focused and efficient threat detection.**


**RBP is a 100-point scale for measuring the relative risk levels of different Events within your environment.** 

- Each Event is assigned an RBP value that can range from 0 to 100, with 0 representing the smallest risks and 100 representing the most severe risks to your organization. 
- **The greater the RBP value of an Event, the greater the priority Analysts should give the Event when qualifying and investigating.** Setting the RBP will help you tune the Event load to a manageable level based upon the number of Events you would like to see on a daily basis in the dashboards. 
- As a general guideline, **only 5% of all collected logs should be forwarded as Events**. You can increase or decrease the RBP scale until you reach your 5% target.


>[! bug]

**Risk settings should be tested before making changes (to ensure that making that change does not stop events from being generated). RBP settings are at the Global level here and will affect all log sources.**


