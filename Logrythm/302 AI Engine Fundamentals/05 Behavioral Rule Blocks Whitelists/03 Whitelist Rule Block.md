### Whitelist Rule Blocks establish approved activity and monitor for deviations.

The Whitelist Rule Block allows you to establish "normal" behavior from virtually any source due to the block's integration with the LogRhythm data filters. After learning what is normal, it compares that against what it sees in your live data. From there you can specify what is accepted or authorized. 

As a result, the block can be used for monitoring servers, applications, users, and network connections. Some use cases include:


## Abnormal User Activity

**Records a normal week, then compares live activity against the Whitelist for abnormal activity:**
  
Using the Whitelist Rule Block, you can monitor a user's activity on a network, server, or application. The Whitelist Profile Block will learn what kinds of activities a user performs, based on log information coming from, or related to, the target that is being profiled. Then you can review that information, modify it, and monitor for any activity that falls outside the established normal behavior.


## Abnormal Processes on a Server

**Records a normal week, then compares live** **activity against the whitelist for abnormal applications, processes, or services:**

A Whitelist Profile Block could be configured to record the list of processes that were launched on a particular server, and optionally which users started those processes. The rule would then create Events or Alarms whenever a process was launched on this server that is not contained in the Whitelist. This could indicate some abnormal behavior on the server, including a virus or other malware attacking the host and launching a set of malicious processes.

*The lab exercise will demonstrate a version of this second use case, only with a smaller time frame.


