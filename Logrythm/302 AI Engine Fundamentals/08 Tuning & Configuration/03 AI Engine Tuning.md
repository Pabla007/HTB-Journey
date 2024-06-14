
AI Engine Rule tuning helps ensure optimal performance of AIE rules. Tuning AI Engine rules will allow you to run more AI Engine rules on the same hardware. 

Given the multifaceted nature of log detection within any rule, it can be beneficial to **narrow the scope of filters and criteria - include exactly what is necessary (everything else will increase processing and reduce the likelihood that it's going to work)**. Both system rules and custom AI Engine rules should be tuned. The following rule settings can be adjusted:

- Day and Time Criteria
- Log Source Filters
- Group By Fields
- Primary Criteria
- Include and Exclude Filters

The key is to **use your use cases to define which log messages are applicable** to your AI Engine rule. Use cases assist in defining required criteria and metadata fields to apply. The better your use case definitions, the better your AI Engine rule which will improve performance but also reduce false positives.

## Primary Criteria Filtering

**Use filters to** **increase** **efficiency.** 

f you create a rule where Common Event "is not nothing," it will look for every single log message identified by the Data Processor, that comes through to the AI Engine. That's every single identified log message! If you have 10,000 log messages a second that are identified...your AI Engine is going to try and compare 10,000 messages/second to that rule! Very inefficient.

Instead, you can make things slightly more specific by changing the primary criteria to "Classification is" a short list of operational issues.

![[Pasted image 20240614092643.png]]


## Exclude Filtering

**Adding exclude filters is one of the single best ways to reduce false positives and improve functionality.**

For example, this DNS Data Exfiltration rule looks at all network traffic and then network traffic that happens after that.

A great thing to add here would be an exclude filter of those locations where I typically send DNS queries. Excluding the top most common DNS queries locations would help improve the rule functionality.


![[Pasted image 20240614092809.png]]


>[! bug] **Important: A Global Log Processing Rule can only tune out metadata being sent to AI Engine – it has no effect on Risk Ratings or any other settings of an AI Engine Event. This is set via the Risk Rating.**

