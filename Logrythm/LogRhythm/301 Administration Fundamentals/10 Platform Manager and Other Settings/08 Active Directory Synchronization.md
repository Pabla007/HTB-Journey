
**Active Directory (AD) Synchronization allows for the synchronization of objects in a Domain(s) with LogRhythm’s Enterprise SIEM.**

**Manage the Active Directory Synchronization** by clicking the Active Directory Domain Manager button from the **Platform Manager tab** in the Deployment Manager.

- Job Manager is the service that will contact the domain.
- The Job Manager service performs a synchronization process every 60 minutes to retrieve data from Active Directory and store it in the LogRhythm EMDB.

![[Pasted image 20240531125933.png]]
AD synchronization allows for domain object synchronization within the Logrythm SIEM


![[Pasted image 20240531125955.png]]


## **After synchronization:**

Access and filter the data using the following tools:

1.  Investigations
2.  Tails
3.  Reports
4.  Personal Dashboard
5.  Alarm Rule criteria
6.  SecondLook restore criteria
7.  Log Distribution Service (LDS) Policy criteria

**You can also view the data from the Active Directory Browsers accessible via the Client Console.** 

You can manage LogRhythm users in the same manner as Active Directory users, allowing you to put users into LogRhythm based on their Active Directory account.


## **Active Directory Synchronization Rules**

- After a Group or User has been created in the local database, it will never be deleted.
- All Users must be synched, or synchronization will fail. Each user is synched independently. If a failure occurs during synchronization, all users synched prior to the failure will have been updated in the database.
- Group membership is synched to reflect membership at the time of sync. All group members must be successfully updated, or no changes will be made for that group. Group membership is updated within a transaction. If any failure occurs when updating a single group, no changes for that group will be updated in the database. However, groups having membership synced prior to failure will have been updated in the database.


