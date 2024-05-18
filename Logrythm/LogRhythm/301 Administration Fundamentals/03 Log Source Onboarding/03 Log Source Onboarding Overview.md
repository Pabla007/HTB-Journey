
```
Log Source Onboarding is the process of accepting logs from different devices on your network.
```


There are various ways of collecting a log source and the methods you use will depend on your environment. See below for each log source onboarding type:

![[Pasted image 20240518170703.png]]


## 1 - Automatic Log Source Acceptance

**For Syslog and Flow Data, which allows for automatic identification and acceptance for Syslog and Flow Data.**  

- Automatic Log Source Acceptance allows the automatic creation of a Log Source Host, Log Source Type, and acceptance of the Log Source. 
- This starts the process of collection nearly immediately.
- Configure it using an IP address range or a regex filter to determine the Log Source Type.
- Your administration time is considerably reduced, by enabling LogRhythm to automatically determine the Log Source Type and accept the Log Source that is collected via Syslog, Flow, and SNMP Trap Receiver.


