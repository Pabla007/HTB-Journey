
```
This tool is especially helpful for larger organizations that might have 50+, hundreds, or even thousands of Agents.
```


- **A System Monitor’s configuration policy determines where and how the logs that it collects are processed.** System Monitor configuration policies are configured and managed via the System Monitor Configuration Policy Manager (pictured to the left), which you can access from the Tools menu of the Deployment Manager. The polices that you assign to your System Monitors should be carefully considered to optimize overall performance.
- **Use the System Monitor Configuration Policy Manager to assign the same configuration policy to multiple System Monitors**. When changes are made to a policy, it updates all System Monitors that are assigned to it.
    - If you have only a few Agents, making configuration changes is usually a small task. If you have many Agents, configuring them one by one can become a burden. Instead, you can create a new policy, add the Agents to a policy, then apply the policy to many of them at one time.
    - For example, you could make a policy for all domain controllers, telling all domain controllers to have the same settings: the same Operating System Type, the same Data Processor they're talking to, etc. Or perhaps you want do endpoint monitoring of User Activity, Network Activity, and Process Monitoring - you could set those three items on one policy, and apply it to all your domain controllers so that they have the same settings.


![[Pasted image 20240515144431.png]]



EXAMPLES

Examples of possible policies:

- Windows 2016 Domain Controller Policy
- File Controller Policy
- Dedicated System Monitor Agent (Collector)



LOCKED AGENTS: INDIVIDUAL CHANGES

Be aware – when an agent belongs to a policy, you **cannot** make changes to Agents on an individual basis.  

If an Agent requires troubleshooting, or you need to make changes to an agent that is in a policy, **it must be removed from the policy first**.



