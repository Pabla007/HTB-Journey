
Before drilling down on an alarm, let's use the Inspector panel to get a general understanding of the alarm and how it was configured.


<hr>


**Here's what I'm thinking:**

I want to learn more about this alarm. To do this, we will need to open the Inspector panel to review the alarm details. I'm specifically curious about what we will see in the AI Engine Rule tab. 


<hr>


**What were the specific rules that triggered this alarm to go off?**
**Inspector Panel: Data, Comments & Details Tab, and** **the AI Engine Rule Tab**

Data, Comments & Details tab and the AI Engine Rule tab in the Inspector Panel:

To bring up the Inspector Panel, click on the Alarm on the Alarms page.

Now we can see the Data, Comments & Details tab.
  
The only field populated from this alarm is the Host Impacted, which is bobsmithlaptop. This is the only field that actually came from the physical log message. Therefore, we'll definitely want to do a drilldown to find the remaining data.

While we are here, let's go over some of the actions that are available:

Clicking on the "View Details" next to Host Impacted would allow us to perform a timeline search on bobsmithlaptop.

Under Alarm Actions, we can change the status of an alarm from open to closed and closed to open. We also have the ability to add to a current case, create a new case, as well as drill down on the alarm.

Under where it says Smart Response Actions section, we can approve or deny that action and add information directly to the case. Finally, in the comments section, we have the option of adding a comment.

Now let's take a look at the AI Engine tab:
  
Here we can see the exact criteria that were used to determine when the rule would fire. For this alarm to have fired, there needed to have been more than 10 logs with the access success and file delete criteria within 1 minute for this rule to fire off an alarm.


<hr>


Now we know that this alarm was triggered because more than 10 logs with access success and file delete criteria occurred within1 minute.

Let's go ahead and drill down on this alarm to learn more about these log messages.


![[Pasted image 20240629225925.png]]


## Drilldown from Alarm Grid View

You can run a Drilldown directly from the Alarm grid view. Do this by clicking on the graph icon to the left of the alarm.


