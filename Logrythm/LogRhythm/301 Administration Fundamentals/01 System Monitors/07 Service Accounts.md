
>Service Accounts
- Running an agent with a service account allows for remote collection and improved security.

**Imagine this remote collection scenario:** 
- Your Agent is on your machine, but you want to reach out and collect logs from a file server. 
- Your Agent _must_ run with an account that has permission to read event logs on the other file server. 
- This can be done by adding a **Service Account**, which has permissions on the other machine's event reader group.

![[Pasted image 20240515113849.png | 400]]

>Consider the account

When installing a System Monitor into a Windows environment, consider the account under which that System Monitor will operate. 

By default, the System Monitor will run using the Local System account, which will give it adequate permissions to gather `local` information. However, it will not have permissions to poll remote hosts for Windows Event Logs.

## Requirements
- **Full control of the installation directory path**
- **HKLM registry key access**(usually given when added to a local Event Readers Group)
- **Needed ports/firewall access** (for example, if you're doing IIS log file collection remotely)
- **Read permissions to target directories or files** (in IIS there is a logs directory - you'd need read permissions to that folder)
- **Membership in the Event Log Readers group** (for Windows Logs)


Specifically, to pull remote Windows logs, the LogRhythm System Monitor service will need to be modified to run under a **named service account**, with **permissions** to access remote Windows Event Logs and other administrative components on a remote machine. This service account will also need to be **added into the Event Log Readers group**, if not already present.


**For a comprehensive list of requirements**, refer to the LogRhythm Software Installation Guide or the Least-Privileged User Guide which is available at [https://docs.logrhythm.com/lrsiem/7.13.0/least-privileged-user(opens in a new tab)](https://docs.logrhythm.com/lrsiem/7.13.0/least-privileged-user).

![[Pasted image 20240515114434.png]]


## Account Permission

Each account that will run a LogRhythm service must have the permissions documented in the LogRhythm Least Privileged User Guide, accessible in the LogRhythm Community.

![[Pasted image 20240515114524.png]]


## Configuring Named Accounts

To configure a named account, use the Services Control Panel found in Windows. Windows accounts must be configured to collect logs remotely from the target systems. If you need more information about using accounts with lesser or least privileges, please contact LogRhythm Support.



## Troubleshooting

If service accounts are used, it is recommended to stop the System Monitor service first, apply the credential changes, and then restart the service.

A Windows Agent requires .NET 4.7.2 which will require a reboot.

The scsm.log file will report if there are issues with remote collection. Access Denied messages will populate with specific host details.

