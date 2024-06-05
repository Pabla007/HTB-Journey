
**What are Global Log Processing Rules?**

GLPRs are like firewall rules – they have an order of precedence. Should a rule match higher up, it will stop processing/inspecting further rules at this point.


<hr>


**Do Global Log Processing Rules affect AI Engine Events?**

No, GLPRs do not affect AI Engine Events. The only way to affect AI Engine is to either use a GLPR to stop sending metadata to AIE or to use the tune features in an AI Engine Rule.


<hr>

**Why might someone use the SecondLook Wizard?**

Use the SecondLook Wizard to restore archived logs for the purpose of further review, audit, or disaster recovery.

<hr>

Which types of data masking are possible in LogRhythm?

**LogRhythm offers 3 types of data masking: Transform, Redact, and Substitute.**
  

**Transform** - Transform specific text within a log message into a specified usable format, where the input text is used to create the output text.
  

**Redact** - Completely redact specific text in a log message where all or part of the input text is replaced with a specified masking character or string.


**Substitute** - Substitute specific text in a log message for a consistent unique value. The data will be hashed into a new unique value where the same input value found in different log messages will always result in the same output value.


<hr>

## **Key Takeaways**

## Data Masking allows for manipulating or altering the representation of log data and is available in three forms, or types –

Transform, Redact, and Substitute. Global Log Processing Rules will apply processing behaviors to incoming logs and provides tuning options to forward logs as Events, override indexing, and override archiving, as examples.


<hr>

For restoring log data back into the LogRhythm Enterprise SIEM from archives, the SecondLook Wizard is available in the Client Console.

