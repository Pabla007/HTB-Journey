
**The final category of AI Engine Rules is made up of Behavioral Rule Blocks.  
Used to detect greater complexity, these rule block types can be more elaborate in their configuration and can monitor for approved log activity deviations, perform statistical correlation, and analyze against trending behavior.


## There are three types of Behavioral Rule Blocks:


1. WHITELIST
**The 'Whitelist' Rule Block will "learn" normal activity, then monitor behavior based on this saved set of normal data.** This Rule Block gives you the option to edit any of the learned activity to refine what is acceptable or approved, so that the result is a list of approved things.


2. STATISTICAL
This combines Threshold and Unique Value Rule Blocks so that you can do both types of things at the same time. 

**The Statistical Rule Block can compare real-time data in a log against a specified value, or to compare two different but related metadata fields.** 

For example, a Statistical Block could inform you when one user changes another user's password by comparing User (Origin) to User (Impacted) metadata.


3. TREND
The Trend Rule Block is similar to the Whitelist Rule Block, but it constantly updates its baseline (whereas Whitelist Rule Blocks learn once and are "done," Trend rule blocks constantly learn & compare, learn & compare). 

**They are used to monitor live log data against a calculated baseline over a specified time period.** Once the baseline has been established, the block can be configured to monitor live data for increased or decreased activity relative to the calculated baseline. 

For example, a Trend rule can be set to monitor production servers and trigger an Alarm when a server exceeds its normal activity due to increased requests from applications or users.


The Behavioral blocks are used to monitor behavior of hosts, users, and other Log Sources that match a filter based on previous behavior or known-good behavior.

These blocks can be used to "learn" to identify normal behavior, configurations, or trending data and utilize complex expressions to evaluate that behavior over time. In some cases, these blocks will trend data over time in a rolling trend analysis; in other cases, a known, set value will be set and used as a comparison point.


## Special Configurations

Each of the Behavioral Rule Blocks contains special configuration options that are much more complex than the configuration of the previously introduced blocks. 

- In Whitelist blocks, a learning mode is enabled.
- In Trend Rule Blocks, a rolling trend analysis mode is enabled.
- In Statistical Rule Blocks, complex expressions are used to compare data in an analytical fashion.

>[!bug ] **Because Behavioral Rule Blocks are more complex, it is recommended that you establish familiarity with how rule blocks in previously covered tiers function first.**

