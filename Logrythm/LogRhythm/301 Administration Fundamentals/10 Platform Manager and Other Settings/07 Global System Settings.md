
### Global System Setting options allow you to set:

1. Backup Paths both relative and UNC
2. Time-To-Live Values (TTL) for online Events or alarm data

![[Pasted image 20240531115445.png]]


Click the **Global System Settings button** from the **Platform Manager tab** to define the **Global Maintenance Settings**. Here you can:

- Enter in the optional backup paths for the various SQL databases. 
- The backup path for the EMDB database **is a must.** 
- Set Time-To-Live (TTL) values that define the amount of time (in days) that different information will be available online  before being removed by the maintenance process.
- Included here is the option to **enable Identity Inference**. 
    - Identity Inference can help recognize the user responsible for an activity when identity information, such as account or login, is not available in the log message. 
    - Using an inference model, the identity associated with logs containing applicable host information, such as IP addresses, can be determined. This feature maintains a mapping of users to hosts based on log activity observed. When this feature is enabled, the MPE performs the identify inference function. 

- _**Note: The Identity Inference feature has been replaced by the TrueIdentity feature. It is not recommended to enable Identity Inference.**_


