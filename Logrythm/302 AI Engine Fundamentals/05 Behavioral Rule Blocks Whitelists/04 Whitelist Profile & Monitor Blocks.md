
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

![[Pasted image 20240609084650.png]]

**The cubic Monitor Block is used after the Profile has been created.** 

- It will monitor live data against the learned Profile of activity, hosts, etc. 
- When data is observed that is not included in the Whitelist Profile, the rule can trigger an Event or Alarm to notify that unusual or unacceptable behavior was detected.


### Viewing the Whitelist

Once the collection interval completes, the Monitor block is used to view and modify the data. The rule will be able to monitor live logs, as they arrive in AI Engine and look for items that do not match the data set defined on the whitelist.

![[Pasted image 20240609084806.png]]


**View a sample collection of Whitelist data below:**

![[Pasted image 20240609084910.png]]

The top line indicates the data collected by this Whitelist. The number of columns will vary with the selection of Group By fields.

As seen in the top line in the image to the left, the data collected in this example was "Process" and "MsgCount" 

Each line item in the rows that follow consist of those two Group By metadata fields.



### Editing the Whitelist

The Whitelist can be manually adjusted from the Profile tab (if set to EMDB) in order to add/remove list entries. 

Take care when modifying a Whitelist. Take note of the format in which the data exists. Be aware that there is additional information captured by the Whitelist that is critical to the workings of the Rule Block. 

### **Recommendations:** 

- Make a copy of a line in the file to use a template, then paste that line at the bottom of the list. Then modify the information in the pasted line to ensure you maintain the correct format of the file.
- If adjusting the Whitelist, it is recommended that you copy a segment and paste it into a text editor in large enough font so that all minor details in syntax can be followed and included.

>[!bug ] Correct syntax is required. **If a mistake is made on line 20 of a 100-line list, only the first 20 lines of data are used by the rule.**
>


### **Use Case: Detect New Host Communication**

This Whitelist Rule is meant to detect changes in host-to-host communication that have not previously been observed. In short, **we want to know which hosts in our network are talking to each other**. 

**Explore the Use Case details below:**


