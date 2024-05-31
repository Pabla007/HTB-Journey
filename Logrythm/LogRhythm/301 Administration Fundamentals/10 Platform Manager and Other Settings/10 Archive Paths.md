
The **LogRhythm Mediator Server** service is responsible for archiving specified log data from a Data Processor database to the LogRhythm Archives.

![[Pasted image 20240531183355.png]]

The Mediator uses configuration parameters that control the way data is archived. Within the **Data Processor's Advanced settings****, you can define the path for both the Active and Inactive Archives.**


## **Active vs. Inactive Archives**

The contents of Active and Inactive Archive files are the same - the original raw log data. Active and Inactive Archive files are written to separate directories to ease the backup of sealed Archive files.

**The differences between the two are:**

1 Active Archive files have not reached the maximum size allowed and are still in the process of having data written to them. The maximum size is configurable.

2 Inactive Archive files have been sealed. Sealed archive files have been hashed for data integrity verification and compressed for storage.

![[Pasted image 20240531183807.png | 400]]


For more information, check out Data Archives and Restoration available at [docs.logrhythm.com(opens in a new tab)](http://docs.logrhythm.com/).


The integrity of LogRhythm archives is preserved, during various stages of processing, through **file attribute monitoring and SHA1 hashing.**

- Archive file attributes and/or hashes are recorded by the LogRhythm Platform for use in verifying integrity during Archive restoration and other operations.
- When Archived logs need to be accessed, the restoration tool, **SecondLook**, allows you to import the logs into a Data Processor database.


## Changing Archive Location

The Archive paths can be modified in the **Data Processor Advanced Properties window.** For best performance, keep Inactive Archives on a file share other than the LogRhythm appliance.

_Note: If you plan to store Archives to a non-local path, the scmedsvr service must be set to run as a user account with permissions to access the specified path. The service account is set via the scmedsvr service properties in the Windows Services control panel._

_Note: High Availability (HA) Network Area Storage (NAS) is recommended for writing Inactive Archives to remote UNC paths._


The LogRhythm Archives are stored, by default, in the S or D:\LogRhythmArchives\Active and D:\LogRhythmArchives\Inactive directories.



