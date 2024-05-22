
Host records can be created via:

![[Pasted image 20240517110731.png]]
Usually, Hosts are created during the agent or log source onboarding process, but they can also be manually created in the Entities tab.


>**System Monitor Agent acceptance**  

A Host record will be created automatically when the System Monitor is installed on a host and accepted into LogRhythm (if there is not a Host record already present).

The acceptance of a new Log Source host occurs when a new Log Source automatically appears in the Log Source queue, or when you add Windows Log Sources using the Windows Host Wizard (described more in the next lesson).

- Recall the prior demonstration: once a System Monitor Agent was accepted, a corresponding Host Record was created within the Entities tab.


>SYSLOG ACCEPTANCE

**Log Source Acceptance**  
For network equipment such as firewalls, routers, and switches, Host records will be added automatically when the device's Syslog feed is accepted as a log source and added into the System Monitor configuration.


>ENTITIES TAB (MANUALLY)

Manually within the Entity tab  
You can add hosts directly in the Entity structure, allowing you to define the Host name, Host Identifiers, and Risk and Threat values. This method is normally used for adding UNIX-based hosts or where System Monitors will not be installed. See below for additional details (this process is similar to the previously described creation of Network Records):


>Adding a Host Record Manually

To add a single Host record:

## Deployment Manager

![[Pasted image 20240517122817.png]]
1. In the Client Console, open the Deployment Manager.

## Entity Tab
![[Pasted image 20240517151136.png]]
2. Select the Entity tab, and then select the Entity to which you want to assign the Host.
## New Host
![[Pasted image 20240517151225.png]]

3. In the Entity Hosts pane at the lower-right of the window, click New, or right-click and select New Host from the context menu. The Host window is displayed.

## Basic Information: Name & Zone

![[Pasted image 20240517151326.png]]
4. In the Host dialog box, open the Basic Information tab, and then enter details for the following:

- **Name** (required): Enter the name assigned to the new host.
- **Host Zone** (required): Select either Internal, DMZ, or External.

## Basic Information: Operating System

![[Pasted image 20240517151530.png]]

- 5 **Continue entering details:**
- **Operating System:** Enter the operating system of the new host.
    - Click next to the Operating System box. In the Operating System Selector window, select the appropriate operating system in the list, and then click OK.
- **Operating System Version**: Enter the version of the selected operating system that is running on the new host.



## Basic Information: Risk & Credentials

![[Pasted image 20240517152017.png]]
- 6 **Continue entering details:**

- **Host Risk Level** (required): This value represents the amount of risk incurred if the system were to become compromised or the subject of some other issue. The Risk level is relevant when the Host is the impacted system, target, or is acted upon by external forces.
    - A value of 0 indicates that no risk is involved in the loss of this system.
    - A value of 9 indicates the highest risk would be incurred if the host were compromised.
- **Windows Event Log Credentials**: If you want the System Monitor to use different credentials for each Host when collecting Windows Event Logs, select the Use specified credentials check box and provide the username and password to be used. If you do not select this option, the System Monitor will use its own service credentials.


## Identifiers Tab
![[Pasted image 20240517152127.png]]

5. On the Identifiers tab, enter Host Identifiers. Identifiers are used by the MPE to associate values in a log message to the correct Host record. Enter all aliases a host may have, but do not enter aliases that are subject to change. For example, a current IP that is assigned by DHCP could lead to misidentified logs because the IP address changes. Available identifiers include:

- Static IP addresses
- Windows names
- DNS names

## Host Roles
![[Pasted image 20240517152229.png]]
6. On the Host Roles tab, enter key contacts for this host.


## Threat Level Tab

![[Pasted image 20240517152331.png]]
7. On the Threat Level tab, designate the amount of threat that is incurred if the host were to be the origin of actions. First, select the Add to Global Source Threat List check box if there is a Threat level greater than 0.

- A value of 1 (low-low) means that actions originating from this host are of little cause for concern or are commonplace. A value of 9 (high-high) means that this host should not be the source of outgoing actions and that there is the greatest threat to security if such events are observed.

## Additional Information Tab

8. On the Additional Information tab, add any other pertinent information. When finished, click OK.

## Log Configuration

9. Now that the host record has been created, we can configure which logs to collect from it. After doing this, our Host may also be referred to as a log source.


## Summary

Giving the Host record as much detail as possible allows everyone using the LR SIEM a greater advantage to understanding better details around a threat or an issue within your environment. This "Derived" metadata gives a cleaner Event Qualification and less False Positives.


