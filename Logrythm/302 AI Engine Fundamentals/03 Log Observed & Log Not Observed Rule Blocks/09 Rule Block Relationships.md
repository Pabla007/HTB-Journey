
AI Engine uses a concept called a **Relationship** to correlate data observed – Group By values from one rule block are compared to Group By values of the next to establish a correlation.

The Relationship concept itself is very simple: **metadata fields of similar type are compared across a given time range.** The Relationship specifies the like metadata information that will be examined by each Rule Block.

![[Pasted image 20240607034432.png]]

For example, Host (Origin) and Host (Impacted) are not identical metadata fields but are of similar type, since information in one can be used in the other.


### The Relationship Time Limit 

The Relationship between Rule Blocks includes a Time Limit.

![[Pasted image 20240607034531.png]]

Located within **Rule Block Relationships,** time limits designate when rule processing starts and stops for successive rule blocks.

## Upper Time Limit entry

The upper entry in the Time Limit specifies **how long the second Rule Block can monitor for matching values**. If the matching log is observed within the Time Limit, the AIE Rule will trigger an Event or Alarm. 

In the example pictured above, this setting indicates that Rule Block 2 has one hour after the criteria in Rule Block 1 is met to identify a matching log before terminating its search.

If a Rule Block locates its matching log in less time than allowed, the AIE Rule will evaluate to true and stop processing. The rule will not continue to run for the full hour; rather, it will proactively stop when the rule is triggered, freeing capacity for other AIE Rules to process more efficiently.


## Lower Time Limit entry

The lower entries in the Time Limit settings can be used to **force Rule Block 2 to evaluate only after Rule Block 1 has completed its monitoring**. 

Normally, both Rule Blocks evaluate simultaneously, and Rule Block 2 could evaluate to true before Rule Block 1 is true. 

If you need the Rule Blocks to be processed linearly, you can simply add a one-second delay between the evaluation of the blocks. However, because all of the rule criteria must be met within the configured time frame, it is uncommon for Rule Blocks to be processed linearly.

