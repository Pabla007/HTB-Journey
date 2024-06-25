
**Beware of false positives. Just because an Alarm was triggered, that doesn't mean it is accurate. Verify why and how the Alarm was constructed.**


In addition to understanding the rule, I should also verify its construction. Analysts should always double check the "facts" given to them.

This means checking and confirming that initially presented information is true. We need to be careful of assumptions. Sometimes mistakes are made.


## Inspector Panel: Check the Alarm's Construction

Let's take a peek at **how** this rule was constructed, so we can better understand:

- **Why** it was constructed.
- **If** it was constructed properly (this helps verify the information being presented).


<hr>


## Prefer to see Dana's steps as a list? Click below!

## AI Engine Rule Tab

**1) AI Engine Rule Tab**  

- **Click** the AI Engine Rule tab. 
This will help us see how the rule is configured, and what the rule is comprised of.



## Inspector Panel: AI Engine Rule Tab - File Sharing Blocked


**2) TE: File Sharing Blocked  
- The top half of the AI Engine Rule tab is labeled: "TE: Cloud File Sharing Blocked." This section tells us:
    - What the rule was designed to do.
    - Why we care about this rule.
- Let's take a closer look.


**3) Classification  
- The Classification was Security/Suspicious


**4) Description & Details**
- The **Brief Description** and **Additional Details** repeat what I just read in the other tab.
- The administrator who built this rule added these notes to show me what this rule is designed to do.
- The rule is meant to tell us about a security event involving attempted file sharing.



## Inspector Panel: AI Engine Rule Tab - Rule Blocks

**5) Rule Blocks**

- The bottom half of the AI Engine Rule tab is the Rule Block. 
- It shows the rule's detection methodology.
- Here, we should evaluate whether or not we think the AI Engine Rule is likely to catch the scenario defined in the description

**6) Log Observed** & **Data Source**

- I see **Rule Block 1: LogObserved** and that the **Data Source** is Data Processor Logs. 
    - In other words, the rule is looking for one log from our Data Processor. This makes sense since the Data Processor is what parses out the metadata for our logs.

**7) Primary Criteria**

- The **Primary Criteria** says the Classification IS Network Deny. 
    - That sounds like what was written in the description: Traffic is being denied to a cloud-sharing site. 
- So far, all this information tells me that the rule's purpose and the rule's actual setup are aligned.
    
- But, does this rule block say anything about cloud sharing sites?
    

**8) Include Filter**

- Ahh, we see in the **Include Filter** that file-sharing sites are blocked.
    - Good. This makes it clear that file-sharing was involved, not just a general network deny.
- So yes, based on the Rule Block, we can have a high degree of confidence that this AI Engine Rule likely captured the correct information.
    
- We should definitely look into this. This can't be ignored or taken lightly; it isn't just a false positive or a misconfiguration.


```
To summarize: we used the Inspector panel to better understand this alarm's purpose and details. 

It gave us an overview of the situation, helped us understand the rule's purpose, and allowed us to verify the rule's construction.  
  
It helped us verify the "facts."
```


## Evaluate Results of Log Collection Practices

Analysts should constantly evaluate the results of log collection practices. Consider:


WHEN & WHY

**When To Evaluate**

- Evaluating the results of log collection practices is not a singular task. 
- Good analysts are always doing this, whether consciously or unconsciously. 
- Every time we drill into data or run a search, we are looking at the metadata, the output, from a log. This gives us the chance to evaluate the collected data.  


**Why Evaluate**

These evaluations should drive our actions as we qualify and investigate: 

- Accurate and useful information will direct us to take certain actions (to make forward progress on the case).
    
- Less helpful logs will lead to taking other actions (such as extra verification steps, looking for unparsed data, or looking elsewhere for additional information), which means slower forward progress.  


These evaluations also help me reflect during the recovery stage, so I can improve for the future.



WHAT TO EVALUATE
**I tend to ask myself three big questions, each with its own subset of questions:**

**1) Is this information** true ?

- Does it make sense?
- Is it accurate?
- Is it expected and typical for my environment?

**2) Is all the information** **there****?**

- Is the information being parsed correctly? 
- Is everything I’d expected to see, actually there?
- Is all the information I require being extracted out of the log?

**3)  Is this information** **useful****?**  

- Is this information going to help me search for possible threats or complete further threat hunting steps?
- Can I use this information elsewhere? I.e. inspect it using AI Engine to look at everybody.
- Can I query on users, hosts, IP addresses with the information from this log? That way, I can contextualize what's going on for this user.



## NEGATIVE EVALUATIONS

> Dana's Advice

Verify Logs & Double Check the Facts.

## Double Check AI Engine Rules

We double-checked that the AI Engine Rule was actually configured in a way that would catch and match the scenario defined in the description.

## Take It a Step Further

We should additionally confirm the PC number and that Adam really is part of the finance team at Telectric.

- Personally, I recognize the PC number and numbering convention; in addition, I know Adam is in finance because we spoke yesterday. 
- How would you verify this information as a new Analyst in the Telectric environment? Where would you begin your search

