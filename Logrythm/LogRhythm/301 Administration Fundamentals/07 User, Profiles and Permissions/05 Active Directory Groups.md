
```
An additional method for granting access to the LogRhythm platform involves creating a User profile and then attaching it to an Active Directory (AD) Group.
```

![[Pasted image 20240529043251.png]]

To use this feature you must:

-  First enter the New Domain Properties in the Active Directory Domain Manager (found in the Client Console’s Platform Manager tab, see picture below).

-  Fully connect The LogRhythm Platform to your AD infrastructure.

-  Make sure the LogRhythm Platform Manager host is a member of the domain, and 

-  That the AD Synchronization Manager is configured to synchronize with the domain.  

-  You must also select the Include in Active Directory Group-Based Authorization checkbox.


![[Pasted image 20240529043515.png]]


