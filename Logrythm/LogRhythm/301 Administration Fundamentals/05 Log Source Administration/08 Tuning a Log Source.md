
```
There are many ways to do this, both before the log message reaches LogRhythm or during processing.
```


![[Pasted image 20240528042818.png]]


**Auditpol** allows the local filtering of events on Windows systems such as the example above or here: **Auditpol /set /subcategory:”Filtering Platform Connection” /Success:disable**

- However, by disabling the event on the local machine, this event will no longer be generated or be able to be collected unless the setting is reverted.

**Syslog/rsyslog settings** allow for the filtering of log messages by priority, i.e. warning and by what logs will be collected.


**Global Log Processing Policy**

If you're certain that you will never need to reference certain logs, there is an option to Filter Raw Logs using the Global Log Processing Policy Manager.  This prevents the System Monitor from ever sending specific logs to the LogRhythm Data Processor.

Global Log Processing Policies will be covered in a later module.


