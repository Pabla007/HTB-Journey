
### Monitoring log activity that is _almost_ identical, apart from one metadata value.

These Rule Blocks are used to monitor for the same kind of activity occurring on several unique items, such as hosts, users, or IP addresses. One set of data in all correlated log messages is the same and **one metadata field in every log message is different**.

In all cases, the Unique Values Rule Blocks will monitor for a set number of unique entries to appear in the correlated log messages.


>[!note] **While this behavior is _similar_ to the Threshold block, the Unique Values Rule Block is monitoring for the same kind of log activity to occur against a set number of unique items, such as hosts, users, or IP addresses.**


## **There are three types of Unique Values Rule Blocks:**

UNIQUE VALUES OBSERVED:
The criteria for these rules are met when the specified number of unique entries is observed in a set of logs within the time range.


UNIQUE VALUES NOT OBSERVED COMPOUND:
The criteria for these rules are met when the specified number of unique entries is not observed in a set of logs within the time range. These can only be used in combination with another rule block.


UNIQUE VALUES NOT OBSERVED SCHEDULED:
The criteria for these rules are met when the specified number of unique entries is not observed as expected in a set of logs within the scheduled time range. This rule must be the only block in the AIE Rule; it cannot be used in a compound rule.


## Unique Value Use Cases

Like the Threshold Rule Blocks, a Unique Values Rule Block can monitor for several items over time. However, **unlike the Threshold Rule Blocks, those items must be different**.

Consider a scenario where a user authenticates over VPN from the **East Coast** and this **same user** generates a VPN authentication log from the **West Coast** within 2 hours.

This may indicate that a user’s account has been compromised or that a user has shared their credentials. Either way, it warrants further investigation.


## One user accesses multiple hosts

When put into context, an Administrator could use the Unique Values Rule Block to detect when a single user accesses 10 different hosts. There would be a Unique threshold value of 10 for the Host (Impacted) field, which would increment each time the user accesses a different host.

For this case to trigger, the user would need to perform the access within the defined time frame.


## Attackers probing the security of a network

When used to track security related information, a Unique Values Rule Block can be set to watch for scanning of a network's outer layers by watching for Reconnaissance type activity that targets 10 unique hosts. Again noting that Host (Impacted) all originating from one Host (Origin) within a very short time frame.


## Operational issues

Another use for the Unique Values Rule Block, specifically the Unique Values Not Observed Scheduled Rule Block, would be to configure the block to look for Backup Complete messages for the number of servers monitored in a data center.

This block would look for a specified number of Backup Complete messages to appear from a specified number of servers within a specified timeframe. If the messages did not appear, then this Rule Block would trigger and could be used to alert analysts that there was a problem with the nightly backup process.

