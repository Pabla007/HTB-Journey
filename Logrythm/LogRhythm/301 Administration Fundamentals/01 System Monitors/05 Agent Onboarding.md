
There are two ways to finalize an Agent's onboarding.

**Agent Acceptance:**  
This is used for brand-new Agents. Once you have installed LogRhythm Agent and configured it, it will start communicating to the Data Processor service. At this time, the Agent will show up in the System Monitors tab with a status of "Pending" (see image below). An administrator will need to select the Action checkbox > right click > Actions > Accept in order for the Agent to start bringing in logs.


**Agent Association:** In other cases, you may need to Associate an Agent. For example: perhaps a host already had software, but the server crashed, was rebuilt, and given the same name and IP. However, because the Agent was reinstalled, it now has a new GUID number. In other words: LogRhythm knows that the machine already exists as a Agent, but it has a new ID number. This is when Agent Association is used. Associating an Agent will connect the old logs to the new logs using the same name.

![[Pasted image 20240514144559.png]]


![[Pasted image 20240515103841.png]]

![[Pasted image 20240515104012.png]]

