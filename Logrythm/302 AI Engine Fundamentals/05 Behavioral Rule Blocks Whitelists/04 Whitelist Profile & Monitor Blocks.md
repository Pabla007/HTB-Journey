
Whitelist Rules are built using two types of rule blocks (they are inherently compound rules):

## Profile Block
The **Profile Block** is where you define what you're going to learn (cylindrical). It is where you learn what is normal. This is where "list population" occurs.

## Monitor Block
The **Monitor Block** is where you compare your live log data to what you learned in the profile block. It identifies activity and behavior outside of what is accepted or authorized. This is where log data is checked against the list.

![[Pasted image 20240609083344.png]]

Whitelist Profile & Monitor Blocks

The AI Engine Rule Wizard will walk you through the tabs to configure the filters used to provide the data to be learned by the Whitelist Profile. You'll recognize most of the tabs, because we've used them to configure other AI Engine Rules. You'll configure the Primary Criteria and any other filters that will be used to build the Whitelist data, including the Log Sources and Day and Time Criteria.

Let's dig into both of these, starting with the Profile Block...


## Profile Block:
The cylindrical Profile Block is used to **analyze and learn normal behavior** about the log data that will eventually be monitored.

This block is used to create the list of approved or acceptable data. The list might include information such as processes running on a host, commands used on a host, users who access a host, etc.

![[Pasted image 20240609083629.png]]

### In the Profile block,_Group__By_ selections specify metadata to be captured and saved in the whitelist.

The **Group By tab** is where you select the contents that will ultimately populate the Whitelist. It specifies which data is going to be on your Whitelist and compared to your live log data. As logs meet the criteria of the Whitelist rule, the metadata field values populate the list.

![[Pasted image 20240609083827.png]]


## Process Name example

For example: if processes on a server will be monitored, **Process Name** would be selected and processes running on the server would be recorded.


## User (Origin) & Location (Origin) example

Another example: if **User (Origin)** and **Location (Origin)** were selected for a Profile block, the Whitelist would populate both field values as logs meet criteria.


**Predict: What happens** if a Group By selection is made but the metadata meant to be detected do not have the field populated?

The data will not be captured and the Whitelist will be blank.


### **Recommendations:**

- In the Profile block, _Group By_ selections are used for data collection, or collection of information that will populate the whitelist. Therefore, **when tuning a Whitelist AI Engine Rule, it is recommended to adjust Primary Criteria or Include/Exclude filters and not _Group By_ selections**.
- Be aware that adding many _Group By_ fields can cause difficulty when managing the Whitelist, so keep it simple.


### The Whitelist Profile Block is configured on the Profile tab.

This tab contains settings for the learning phase of the Whitelist rule.

![[Pasted image 20240609084141.png]]


## Profile Tab view for a Whitelist Rule Block

COLLECTION INTERVAL

This will help you define the Collection Interval, or time frame, used to specify **how long AI Engine will spend collecting the Whitelist Profile data**. This time frame can be set to a few minutes or several days.

More time spent looking at normal behavior might yield a more accurate reflection of what is occurring, but might also begin to include anomalies or one-offs that are not actually normal behavior. Keep in mind the data you are looking to monitor, so that you can build your profile accordingly.


# STORAGE

Profile Storage is the location **where the** **collected Profile information will be stored**. There are two options in the Storage Area drop down list:

- **EMDB**: This is selected by default and _it is not recommended that you change it_. This will write the saved data directly into the Event Manager Database (EMDB). The View Data button will become active after the Profile data collection has completed.
- **Baseline**: This option will write the captured Profile information to a CSV file stored in the AI Engine Server's software installation directory. Using Baseline is not recommended as access to CSV files is unavailable.

While the option to adjust the Storage Area and the Storage Name are _technically_ available, do not change either. If the Storage Name is modified, the block will not record data.


Once profile data collection is complete, the Whitelist is available to view. You can use the **Monitor Block** to make adjustments.


## **Monitor Block**
