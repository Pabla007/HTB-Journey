
### The key to the Threshold Rule Blocks is specifying the value which must be observed or not observed. 

The threshold values are defined on the Thresholds tab. The Threshold Rule Blocks allow for great flexibility because you can choose to specify a threshold on one or more items.


## The following types of data can be used in Threshold Rule Blocks:

- Log Count
- Host (Impacted) KBytes Received (a raw incremental value)
- Host (Impacted) KBytes Sent (a raw incremental value)
- Host (Impacted) Kbytes Total (a sum of the raw Kbytes in or out)
- Host (Impacted Packets Received (raw number of items; often found in email and VOIP logs)
- Host (Impacted) Packets Sent (raw number of items; often found in email and VOIP logs)
- Host (Impacted) Packets Total (a sum of the above information)
- Duration (how long something was running for, typically found with process or job information)
- Amount (amount of an item; could be a dollar amount or some other amount) and Quantity (Quantity of an Item/Object)
- Rate (the rate of an Item/Object) and Size (the size of an Item/Object)


![[Pasted image 20240608025541.png]]


## Time Limits

Located on the Threshold tab of a Threshold Rule Block, the Time Limit settings allow you to specify a maximum timeframe in which the threshold is to be reached in order for the Alarm to trigger. If the criteria for the Threshold rule is not met within that limit, the rule stops processing.


![[Pasted image 20240608025643.png]]
Time Limit setting within the Threshold Rule Block


>[!bug] While it is _possible_ for thresholds to be set to monitor for days, you should **use caution when setting a long Time Limit** in your Rule Block because it will require additional memory in order to function and may not be efficient.


**What do you think?**

Which time limit should be shorter?

- [x] Relationship Time Limit

- [ ] Threshold Rule Block Time Limit


Nice try! The **Threshold time limit should be shorter than the Relationship time limit**. That way — in the event that a threshold is not detected within the threshold time limit — a new instance of the threshold can monitor for the remaining time of the rule.



### **Threshold Time Limits vs. Relationship Time Limits**

When a Threshold Rule Block is the second or third block in a rule, the Threshold Time Limit and Relationship Time limit work independently from each other.


## Relationship  Time Limit

The **Relationship Time Limit** sets a boundary for how long the Threshold Rule Block is allowed to execute overall.

## Threshold Rule Block  Time Limit

The **Threshold Rule Block Time Limit** settings define the time allowed from when the first matching log is observed, to when the threshold value is exceeded.

<hr>

**You would not want to set a Threshold Time Limit to evaluate for longer than the Relationship.** If the time passes and the threshold has not been triggered, then it is evaluated as false and the Rule Block stops processing.

This is a critical concept when using AI Engine. Even if a Threshold Rule Block is created and begins to evaluate logs, the fact that it did not trigger within its time limit will not prevent the AI Engine Rule from continually evaluating the Threshold Rule Block.


## For example:

**Let's say the Threshold Time Limit is set to 10 minutes with a Relationship Time Limit of one hour.**

The Threshold Rule Block will be given time to observe the logs, then will stop if the threshold is not met.

If another log that matches the threshold configuration appears within the one-hour timeframe (even if a previous Threshold Rule Block failed to trigger), a new Threshold Rule Block process would begin. It would monitor for additional logs until the threshold is met, provided that the Relationship Time Limit had not been exceeded.


<hr>

## Use Case: Data Theft via DNS tunneling

DNS Tunneling is a method of cyber-attack that encodes the data of other programs or protocols in DNS queries and responses. DNS tunneling often includes data payloads that can be added to an attacked DNS server and used to control a remote server and applications. 

The normal use for this, apart from to bypass Hotel and Airport WIFI, is to use it for Data Exfiltration where the Upstream DNS requests are not restricted. The idea behind this use case is that normally UDP DNS traffic is more or less about 100 bytes in size. As we are using the first part of a DNS request to send encoded data the packet size will increases to 200 bytes or more in size which is a sign of something unusual happening.


![[Pasted image 20240608033132.png]]



## Additional info

[(opens in a new tab)](https://attack.mitre.org/techniques/T1048/)(External links)

- [**MITRE’s ATT&CK Technique T1048**(opens in a new tab)](https://attack.mitre.org/techniques/T1048/)
- [**Iodine**(opens in a new tab)](https://github.com/yarrick/iodine) – an example tool for DNS tunneling
- [**National Chocolate covered Cherry Day**(opens in a new tab)](https://www.daysoftheyear.com/days/chocolate-covered-cherry-day/) – Events like this can be used as Social Engineering Phishing attacks. They are attempts to get the user to engage with the malicious link or code.[(opens in a new tab)](https://github.com/martinoj2009/ICMPExfil)
- [**IMCPEXfil on Github**](https://github.com/martinoj2009/ICMPExfil)



**What other use cases** can you think of for Threshold Observed Rules?
An increase in error logs for a server might be indicative of an Operational error or possibly a DOS attack.


