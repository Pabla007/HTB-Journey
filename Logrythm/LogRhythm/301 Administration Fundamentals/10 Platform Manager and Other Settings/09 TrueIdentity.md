
```
TrueIdentiy should be configured if you use Active Directory.
```


**TrueIdentity allows for the aggregation of multiple user identifiers into a single identity such as user accounts and email addresses.**

This is shown in the example below for Bob Smith.


![[Pasted image 20240531183002.png]]

TrueIdentity has a one-to-many relationship, i.e. you have a root or base user profile, and then multiple other identities are related to this primary identity.

**TrueIdentity allows you to track and monitor user-based activity and link disparate user identities to a single base or root identity.** 

This allows you to **spot malicious activity more easily,** such as:

- Malicious insider threat
- Compromised accounts
- Privilege abuse and misuse
- Brute force attacks
- New privileged accounts
- Unauthorized data access and exfiltration

TrueIdentity is configured using the TrueIdentity Synchronization tools in the Web Console.

The TrueIdentity Sync tool allows you to pull in Active Directory information from a Domain and use this user information to form the basis of your user entity structures.

**If you have a multi-tenant environment, go to [C:\Program Files\LogRhythm\LogRhythm Mediator Server\config(opens in a new tab)](http://c/Program%20Files/LogRhythm/LogRhythm%20Mediator%20Server/config), and set the EnableIdentityEntitySegregation parameter in the scmedsvr.ini to True.**



