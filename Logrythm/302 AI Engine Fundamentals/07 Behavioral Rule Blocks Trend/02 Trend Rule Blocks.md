
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