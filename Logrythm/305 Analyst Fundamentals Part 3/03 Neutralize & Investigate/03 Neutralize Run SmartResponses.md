
SmartResponses are prebuilt scripts that allow you to execute actions without leaving the Web Console.


## Approve a SmartResponse from an Alarm

From the Cases page:
1. Select the alarm.
2. Open the Inspector panel.
3. Click the "approve" button from the SmartResponse section of the Inspector panel.


<hr>


## Running a SmartResponse Manually

1. In the Analyzer grid, click the **Cog icon** in the cell that contains the metadata that requires a SmartResponse.
2. In the Inspector panel's SmartResponse section: 
    - Click the **Plugin dropdown** and **Action** **dropdown** and select from available SmartResponse actions.
    - Note: SmartResponses are permissions-based. You may need to submit credentials.
3. Review and verify your SmartResponse using the **Command to Execute box**.
4. In the **Execute From** **dropdown**, select a location from which to run the SmartResponse.
    - You can run it from the Platform Manager, which is the default, or any System Monitor Agent within your entity.
5. Click **Run**.





GATHER DATA

**SmartResponses can** **provide deeper forensic or operational data**.   
For example:
- After an alarm is generated from a compromised system, a SmartResponse can initiate a vulnerability scan or packet capture on the target host.


AUTOMATE TASKS
**SmartResponses can a******utomate operations tasks******.**   
For example: 

- When an alarm is triggered, a SmartResponse can automatically create a case and add a tag to it.
- After a critical operations issue is observed on a network device, a SmartResponse can automatically set the device to debug-level logging.


DEFEND
**SmartResponses can i******mp**lement security controls in defense of an attack or intrusion**.   
For example:

- After observing near concurrent successful logins using the same account from two different countries, a SmartResponse can disable the account.
- When an inappropriate process is detected on a server, such as BitTorrent or a Peer2Peer application, a SmartResponse can kill the process.



## SmartResponses from Alarms

**SmartResponses can trigger from an alarm.**  
If your Alarms page is set up in "Card View" you can see the status of any SmartResponses right on the Alarm Card.

- **Not Set** - displays if no SmartResponses are configured to that Alarm.
- **Succeeded** - displays if an automatic SmartResponse was executed.
- **Failed** - displays if an automatic SmartResponse was unable to execute.
- **# SmartResponse Action**- Sometimes you may want a SmartResponse to be easily accessible from an alarm, but not automatic. In this case, you'll see how many SmartResponses are available. To run them, simply:
    - Select the alarm card.
    - Open the Inspector panel.
    - Click the "approve" button from the SmartResponse section of the Inspector panel.

