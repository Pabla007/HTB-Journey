
The Statistical Rule Block evaluates log messages over time (as opposed to in real-time) by comparing real-time metadata against a specified value or two different but related metadata fields. It analyzes those log messages using mathematical expressions to detect anomalies or abnormal behavior.

Simply put, it combines the functionality of a Threshold rule block and a Unique Values rule block into a single rule.

**For example**: a Statistical rule can be configured to monitor for 10 or more Authentication Failure logs from the same User (Origin) on at least 5 different Hosts (Impacted) within 20 minutes.


In the described example, which attributes are Threshold vs. Unique Value attributes?
Threshold is the time frame of 20 mins
Unique Value is the Authentication Failures from the different Hosts

Is "Authentication Failure" a Classification or a Common Event?
Classification

Does "Authentication Failure" sound general or specific?”
Specific


>[! note] For Statistical rules, we no longer evaluate in real time. We collect logs and evaluate at scheduled intervals.

