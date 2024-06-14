
**A workload is a set of AI Engine rules. Workloads can be used to further tune AI Engine.**

## What is a workload?

An AIE Workload is a pre-defined filter between the Data Processor and AI Engine Comms manager which manages which data is sent to AI Engine for inspection.

In other words: it is a rule container within the LogRhythm platform that specifies all AIE rules available for use by a given AIE server. It is comprised of one or more rule sets.


## What is a rule set?

AIE Rule Sets allow for the gathering of rules into a group (or set) as well as for providing a filter to specify which logs will be sent to the rule set's workload.

All logs are sent to the AI Engine by default unless one or more Include and/or Log Source filters are specified at the Workload or Rule Set level. If Include filters are specified, at least one Include from the Workload or Rule Set must match.

## Why are they helpful?

A workload is inspected before metadata gets to the AI Engine Service – i.e., it is a predetermined filter between AI Engine Comms Manager and the Data Processor

Because workloads allow the filtering of data before AI Engine inspects it, performance can be improved considerably.

Tuning using Log Sources means all log sources are still being inspected (Metadata from the log) however the filtering is happening after it receives all the data.


## Examples

Examples of Workloads:

- Enabled AI Engine Rules only (see Recommended Practices below)
- Web Server Workload – i.e., cross site scripting, SQL injection rules only


## Location

The **Workloads tab** can be found at the bottom of the AI Engine tab grid within the Deployment Manager.

