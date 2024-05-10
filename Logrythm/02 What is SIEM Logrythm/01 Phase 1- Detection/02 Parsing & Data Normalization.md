
```
When log sources speak different languages, the SIEM is your translator. Parsing and Data Normalization are about creating a consistent language for comparison.
```


>Key Terms in this lesson:
- Metadata
- Parsing
- Data Normalization
- Detection

## **What's metadata?**

**Metadata** is data about the data (log message). Log messages contain data, and the SIEM can extract data about the log messages.

There are 3 types of metadata in LogRhythm SIEM:

1. **Contextual Metadata:** Parsed directly from the log message, contextual metadata is text-based and descriptive.  
      
    _Examples: Login, Account, Vendor Message ID, Sender, Recipient, Subject, Object_
2. **Quantitative Metadata:** Parsed directly from the log message, quantitative metadata can be used for numeric comparisons._  
      
    _Examples: Bytes in/out, Items in/out, Duration, Size, Quantity, Amount, Rate__
3. **Derived Metadata:** Using parsed metadata and relating it to the LogRhythm configuration information, derived metadata adds additional context.__  
      
    _Examples: Origin Network, Impacted Network, Origin Known Host, Impacted Known Host, Origin Zone, Impacted Zone, Direction___


Every log message is assigned a classification based on the metadata extracted from the message. Classifications help group common events. There are 3 classification types:

1. **Audit:** An example of an audit-oriented classification is Authentication Success.
2. **Operations:** An example of an operations-oriented classification is Network Traffic.
3. **Security:** An example of a security-oriented classification is Reconnaissance.



Common events are assigned to each log message to further describe the activity. Where classifications describe the broad range of activity, common events provide more descriptive context.

Here you will see categorization in order of largest to smallest from left to right:

**Classification Type > Classification >** Common Event examples

1. **Audit > Authentication Success >** User Logoff/Logon, Computer Logoff/Logon  
    
2. **Operations > Network Traffic >** Connection Attempt, Connection Closed, Connection Lost, Connection Request
3. **Security > Network Traffic >** Ping Sweep, Port Scan, Traceroute Activity, Vulnerability Scan



## **How does a SIEM parse a log?**

Once the log data has been collected it is forwarded to a processing engine. The processing engine extracts metadata from each log message. It organizes the metadata in human-readable spreadsheet format.

**Parsing** is the process of extracting metadata from a raw log message.



## **What is Data Normalization?**

The SIEM can perform time normalization to standardize timestamps from different time zones. When the log data is parsed for metadata fields, the timestamp is corrected to reflect the time zone where the SIEM appliance is located.

This process enables an Analyst to quickly see what is happening and focus on investigating an event.

Read more about other forms of Data Normalization below:
![[Pasted image 20240511020048.png]]

![[Pasted image 20240511020103.png]]

![[Pasted image 20240511020129.png]]

![[Pasted image 20240511020150.png]]

## **Detection, Parsing & Data Normalization**

If two systems use different metadata field names for the same information, the SIEM employs **Parsing** and **Normalization**. This ensures consistent categorizaion of the information under a single metadata field. 

**Data N****ormalization** is about uniformity and consistency. It allows the SIEM to interpret various languages used by different log sources and translate them into a unified language.

**Parsing** and **Data Normalization** enable the **detection** of problematic patterns in the data, making it possible to identify and address issues effectively.


![[Pasted image 20240511020426.png]]


```
To learn more about LogRhythm's parsing tools, visit [https://docs.logrhythm.com/lrsiem(opens in a new tab)](https://docs.logrhythm.com/lrsiem/) and search RegEx, **Data Processor, or** **Message Processing Engine.**

**For LogRhythm's Data Normalization tools, search Data Processor, Metadata Fields, or Normalization.**
```

After adding a filter we get a objectname herman@HTB.local who has write access.
![[Pasted image 20240511021329.png]]


```
ObjectName	ObjectType	ObjectGuid	PrincipalName	PrincipalType	ActiveDirectoryRights	ACEType	AccessControlType	IsInherited

herman@HTB.LOCAL	USER		nico@HTB.LOCAL	USER	WriteOwner		AccessAllowed	False
```

And Tom has write write access onver clair
![[Pasted image 20240511021637.png]]

And if we search with a Claire than we can say that it has access to Backup_Admins@HTB_LOCAL
![[Pasted image 20240511021845.png]]

