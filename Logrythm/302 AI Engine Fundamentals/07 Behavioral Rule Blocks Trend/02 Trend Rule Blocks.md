
### **By constantly learning and comparing, these rules are helpful in seeing spikes and drops in log data behavior.**

Much like the Whitelist Rule Block, Trend Rule Blocks use a Profile-like learning mode to establish a baseline, and they require the configuration of a second Rule Block.

- Monitor Block- the current trend of incoming data is compared against the baseline data.
- **Baseline Block** - the Baseline Block is similar to the Whitelist's Profile Block. Both cylindrical blocks "learn" what is normal over a given period of time and then compares the live log data to what was normal.


![[Pasted image 20240609104443.png]]


>[! note]
>**The main difference between a Trend Rule's Baseline Block and a Whitelist's Profile Block is that a Baseline Block continuously updates itself and forgets old stuff. It uses a rolling baseline.**


## A Rolling Baseline

Trend Rule Blocks use a concept of a rolling baseline. This baseline will dynamically add new logs that match the Rule Block's criteria back into the baseline; this data can be used immediately for trending against the evaluation period.

The Trend **Base****line configuration must be completed prior to the Trend Monitors block configuration.** Like the Whitelist block, the Trend Block can be automatically configured to share the same data filter as the Baseline block, or it can be custom configured with a separate filter. Usually, the two configurations are the same

## Organizational Familiarity

When using Trend Rules, it is important to become familiar with how your organization operates with respect to work schedules and holidays (as examples) in order to reduce the likelihood of false positives


## Use Case

For example, a Trend Rule Block can be used to monitor user access to files for more frequent than normal activity.


### Use Case: Server Load Comparison

For example, an Administrator may want to create a Trend Rule to monitor a critical server for its overall load, and to create Events and Alarms when the load on the server exceeds four times the normal load.

**Configuration**: The Administrator creates a new AI Engine Rule using the Trend Rule Block. The filter for this block is set to monitor all activity on the one host. This includes all user activity, authentication and access activity, operational activity including errors and warnings, and any other information that can be associated to that host.

- The Administrator then configures the **Data Fields** to be the Log Count (how many logs have been observed related to this host).
- The Administrator configures the **Group By** fields to include the Host (Origin) and Host (Impacted) fields.
- The Administrator configures a four-hour **Baseline Time Period** with a one-hour **Live Time Period**.
- On the **Expressions** tab, the Administrator adds the Log Count Comparison expression. It also configures it to trigger if the number of logs observed in the Live Time Period is at least four times greater than the number of logs observed during the Baseline Time Period.

This Trend Rule will create new Events and Alarms, if the critical server appears in logs at a rate that exceeds four times the "normal" average log volume as measured by the rolling baseline. As soon as the load on the server falls within the Baseline value, the Events and Alarms will stop being generated.


<hr>

## Use Case: Rogue HostDetection

This Trend Rule Use Case is looking for new rogue hosts being added to the network. 

The trend rule collects known hostnames over a 3-day period and then evaluates this against new data collected every 4 to 8 hours and alerts on any changes. These new hosts could be endpoints, WIFI devices such as access points, DHCP Servers etc. 

You could add some tuning here such as, you use Dell equipment, and you wish to exclude these Mac Addresses by their OUI’s.

![[Pasted image 20240612171649.png]]


## **What other use cases can you think of for Trend Rules?**

Answers will vary. For example: unusual Spike in Log Generation from a Server – indicative of either misconfiguration or maybe a DOS attack.

Other examples include:

- Web Server DDOS Attack
- Rogue Host Detection
- Abnormal Origin Location
- Abnormal File Access
- Abnormal Amount of Audit Failures
- New Common Event
- Abnormal Log Volume Fluctuation


## Resources

External links for further reading and reference:
- [(opens in a new tab)](https://attack.mitre.org/techniques/T1135/)Go to [**MITRE ATT&CK Rogue Wi-Fi Access Points**(opens in a new tab)](https://attack.mitre.org/techniques/T1465/)[(opens in a new tab)](https://attack.mitre.org/techniques/T1465/)
- Go to [**MITRE ATT&CK Rogue Cellular Base Station**(opens in a new tab)](https://attack.mitre.org/techniques/T1467/).  
- Go to [**MITRE ATT&CK Host Based Hiding Techniques**(opens in a new tab)](https://attack.mitre.org/techniques/T1314).
- Go to [**Github for WIFIPhisher a Rogue WIFI Access point**(opens in a new tab)](https://github.com/wifiphisher/wifiphisher).



## Knowledge Check

Trend Rule Blocks compare live log data against a stored baseline to detect variances over time.

Trend Rule Blocks utilize a two-block setup, consisting of a _Baseline_ and _Monitor_ Block. 

An example of a Trend use case would be monitoring for file access activity that is more frequent than normal.


## Each Behavioral Rule Block includes time setting options to apply during their configuration.

- The Whitelist Rule Block has a _Collection Interval_ setting in the Profile tab that determines how long the rule block will record behavioral data to be included in the Whitelist. 
- The Statistical Rule Block has a _Time and Schedule_ tab that will include settings for the _Live Time Period_, the _Evaluation Frequency_, and the _Evaluation Schedule_. 
- The Trend Rule Block also has a _Time and Schedule_ tab, but with a _Baseline Time Period_ in addition to the _Live Time Period_, _Evaluation Frequency_, and _Evaluation Schedule_. 

Time settings for Behavioral Rules should be tuned in order to balance between rule effectiveness and system resource availability.


