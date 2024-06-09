
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


## 

Organizational Familiarity

When using Trend Rules, it is important to become familiar with how your organization operates with respect to work schedules and holidays (as examples) in order to reduce the likelihood of false positives