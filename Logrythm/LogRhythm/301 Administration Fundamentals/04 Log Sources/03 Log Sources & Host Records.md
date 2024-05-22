
```
Every Log Source requires a Host Record.
```


EVERY LOG SOURCE REQUIRES A HOST RECORD

**Every Log Source is associated to a Host Record** in the Entities tab.

- Generally, host records must exist before you can configure a new Log Source (WEF is an exception - WEF doesn't create a host for each log feed coming in. There is a single WEF server listed as a host, but not the individuals sending data.)
- Many log sources can automatically create a new Host Record (e.g. Syslog sources) via log source onboarding.
- Note: While one host can contain several log sources (e.g. Application / Security / System), the reverse is not true. One log source cannot belong to multiple hosts.


<hr>


WHY DO THEY HAVE TO BE ASSOCIATED?

The Host record association allows you to adjust the importance of logs via LogRhythm's Risk Based Priority (RBP) Event forwarding. You can use the Host record's Risk and Threat ratings to adjust the importance of a log. Each Log Source attached to a Host record will be adjusted by these ratings to be more, or less, important than normal, depending on the settings for the host.

- For example, your firewall and domain controller logs may be more important, and you can change those host record risk and threat records to influence that value.

The Host record association helps derive important metadata from a log (such as Known Host, Impacted Host, or Origin Entity) based on the information found in the Entities tab.



