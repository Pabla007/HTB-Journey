
### **The AI Engine Rule Block Wizard contains a tab called Unique Values for use in the configuration of Unique Values Rule Blocks.**

In this tab, you are asked to choose a setting from the Field drop-down menu. This setting can be any field _not_ selected on the **Group By** tab. In addition, the number of Occurrences (like a threshold) must be specified for the number of Unique Values that the rule is looking to observe. (See image below.)

![[Pasted image 20240608035653.png]]

In this picture, **Host (Impacted)** has been selected. With the **Occurrences threshold set to 10**, this Rule Block will monitor for 10 different Impacted Hosts in the correlated logs that matched the filters configured in the Primary Criteria, Include Filters, and Exclude Filters tabs.


## Group By tab

Remember, the **Group By** tab is used by AI Engine to define the Relationship of data between Rule Blocks. It is used to pass information about one log to another inside a single Rule Block, as well as pass that same information to a second or third Rule Block.

The **Group By** configuration is used by a Rule Block for Aggregation purposes as well. When logs are matched by the data filter, they may contain varying metadata elements, such as different hosts in the Origin or Impacted Host fields. Ensure that the Rule Block is always evaluating the same Origin or Impacted Host (for example) by selecting both fields in the Group By settings. In other words, if two hosts were to report the same activity, the Rule Block would evaluate each host separately when the setting described above was enabled. If Origin and Impacted Host were not checked in the Group By settings, the two hosts would be evaluated together, resulting in a rule that may not correctly evaluate the condition you desire.



### **Use Case: Detect Password Spraying**

Password Spraying is a type of brute force attack where a hacker tries to gain access to an organization's systems by testing out a small number of commonly used passwords on a large number of accounts. The assumption with that is that, within a large group of people, there is likely to be at least one person using a common password. There are two scenarios for password spraying attacks:

1st Scenario:
An endpoint has been compromised and the malicious actor wishes to try and elevate their privileges by targeting known Domain Administrators or IT Administrators (Exchange, MS SQL, Linux Administrators etc.).


2nd Scenario:
An alternative way of using password spraying is where a malicious actor uses their own infrastructure against your Cloud Services Infrastructure such as Office 365. Normally this takes the form of a low and slow attack i.e., one password attempt every 24 hours.

![[Pasted image 20240608040039.png]]

(External links)

- [**Command line logging for Windows**(opens in a new tab)](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/component-updates/command-line-process-auditing)
- [**MITRE ATT&CK Technique T1110 and the four sub techniques**(opens in a new tab)](https://attack.mitre.org/techniques/T1110/)
- [**MITRE’s ATT&CK Technique TA0006**(opens in a new tab)](https://attack.mitre.org/tactics/TA0006/)
- [**myBFF, an example tool for Brute Force Password**(opens in a new tab)](https://github.com/rapid7/myBFF)
- [**Specops Password Auditor**](https://specopssoft.com/product/specops-password-auditor/)


## Further Reading and Reference

(External links)

- HoneyPort – PowerShell Honeypot on GitHub: [**https://github.com/Pwdrkeg/honeyport**(opens in a new tab)](https://github.com/Pwdrkeg/honeyport) 
    
- PowerShell Logging: [**https://docs.microsoft.com/en-us/powershell/scripting/windows-powershell/wmf/whats-new/script-logging?view=powershell-7**(opens in a new tab)](https://learn.microsoft.com/en-us/powershell/scripting/windows-powershell/wmf/whats-new/script-logging?view=powershell-7.3&viewFallbackFrom=powershell-7) 
    
- PowerShell port scanning: [**https://techcommunity.microsoft.com/t5/itops-talk-blog/powershell-basics-how-to-scan-open-ports-within-a-network/ba-p/924149**(opens in a new tab)](https://techcommunity.microsoft.com/t5/itops-talk-blog/powershell-basics-how-to-scan-open-ports-within-a-network/ba-p/924149)


