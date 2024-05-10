
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