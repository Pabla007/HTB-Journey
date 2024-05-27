
```
Unidentified log detection using Investigations, Searches, and Reporting
```

**An Unidentified Log** is a log that has been sent to the Message Processing Engine (MPE) but was not identified by any of the MPE Rules. **The most apparent indicator of an unidentified log is that it does not carry a Classification or a Common Event.**


**This issue most likely oc****curs when:** Adding custom Log Sources for which custom regular expression parsing rules have not been created or an Administrator added a Log Source using an incorrect Log Source Type.


**Repair:** Discovering unidentified logs allows you the opportunity to create custom rules or to correct the configuration. This can help reduce the impact to MPE performance while also improving metadata field population within parsed logs.

![[Pasted image 20240528020726.png]]


The Client Console contains the following tools that can assist in discovering unidentified log occurrences:

**Investigations & Searches:** Perform a search for logs which have no Classification or Common Event assigned. Those logs were not identified by LogRhythm.

**Reports**: Log Volume reports provide statistics, by Log Source, that will show the percentage of logs being identified. Anything less than a 100% identification rate should be investigated.

