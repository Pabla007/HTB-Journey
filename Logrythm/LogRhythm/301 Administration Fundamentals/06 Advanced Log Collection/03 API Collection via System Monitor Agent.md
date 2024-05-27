
Let’s look at some of the common troubleshooting methods for API Log Collection. API collection is for a set of support devices; the API is normally a REST API which uses some form of authentication such as:

- Username/Password 
- OATH2 or JWT tokens **or**
- API Keys such as a Client_ID and Client Secret 

Normally the agent needs access to the endpoint via https, but this is dependent on the API Service.


>API Collection

![[Pasted image 20240528050329.png]]

>API CONFIGURATION

See an example API configuration below. Everywhere that you see CHANGE_THIS needs to be modified.

All of the .ini config files for SysMon API log sources are located here:

**C:\Program Files\LogRhythm\LogRhythm System Monitor\config**

![[Pasted image 20240528050411.png]]



>API SETTINGS (INI) FILES

**Be aware:** Remote collection can be throttled by the service, i.e. Azure throttles the number of logs that can be collected by the service that is subscribed to it. API Data throttling is common.

![[Pasted image 20240528050517.png]]


**API configuration guides are available in LogRhythm Docs. Make sure you are signed in to Docs, then** [**CLICK HERE** (opens in a new tab)](https://docs.logrhythm.com/devices/docs/api-log-sources)**to access them.**


## **API Troubleshooting**

Tools like Wireshark and Fiddler can be invaluable when debugging a connection to a web service. These tools allow you to see all the different network connections that your system is making and can also allow you to view the information that is being sent to the service. This can be helpful for cases where you want to see what exactly is being sent.


![[Pasted image 20240528050716.png]]


These are 3rd party tools for connectivity testing. This testing should be done from the Host with the installed Agent that is having issues with collecting the Log Data. 

For some services, the API is not available by default and would need to be turned on via the 3rd party, i.e. QUALYS.

**Note**: This module covered using API as a Log Source. We will go over how to interface with the LogRhythm environment using API in a later module.


