
**Recovery is a crucial phase of TLM.** **It is all about improvement. How can we prevent similar situations? Respond faster? Be more efficient?**

![[Pasted image 20240625022428.png]]


HOW YOU CAN IMPROVE

**Reflect:** When closing a case, always ask yourself how you could have done it differently and more effectively.

**Revise:** Remember how we noticed that the Dropbox's URL didn't parse correctly? That is something we will need to improve.  

**Document:** Record your reflection and improvement ideas in the case comments.


<hr>


QUESTIONS YOU CAN ASK

**At the end of a case, I ask myself questions such as:**

1. Were there any steps that took longer than I expected? If so, why do you think that was the case?
2. Was there anything else that should've been done?
3. What are some proactive things we can do to position ourselves to respond faster and more comprehensively next time?


**Improvement #1: Log Collection Practices**

**Recovery gives us the opportunity to reflect on our log collection practices.** 

Did everything show up as expected or were things missing or incorrectly parsed?



## Verify Logs

We could add comments about the results of our log collection practices.

- **Log Verification**: We already did this thinking along the way as we noticed whether log data was true, complete, and useful; that's how we noticed the Dropbox URL not parsing. 
- **Parsing Issues:** We should take note of that parsing issue here, as well as any other needs identified from that constant evaluation process.


## Uncollected & Missing Logs

We could add comments about the logs we're collecting. For example, I ask myself:

- Is the information I'm currently collecting useful enough that I want to continue collecting it?
- Is there something that we should have collected that would have made this case go more quickly, easier, and better? 
    - Am I missing any helpful logs?  
        
    - Are there any logs that I’m not seeing, that I want to start seeing?



## Uncollected & Missing Logs: Examples

I'm not missing much. I have DNS and firewall logs. However, I'm missing some things that would make my life easier. 


**Command Line Logs:** 

- I have some PowerShell logs, which is great. However, Where are my Command Line logs? Not everything is in PowerShell. 
    
- Command Line Logging is a type of enhanced auditing to capture commands that are manually typed in. They can be found within the Windows Application Log.  
    
- To learn more about PowerShell and Command Line logs, visit [logrhythm.com/blog/powershell-command-line-logging/(opens in a new tab)](https://logrhythm.com/blog/powershell-command-line-logging/)
    


**Microsoft Set Up Logs:** 

- I'd expect to see standard Microsoft setup logs. 
    
    - These logs would help me see if, and when, any applications have been installed. 
        
    - These logs would help me understand timelines.
        
- This would have helped me in the context of the PowerShell process. 
    
    - I would have seen it being installed, where it was installed, and if it was a temporary file. 
        
    - This would have more quickly brought me to the realization that Adam didn't go to Dropbox, and that something else happened.



# **Improvement #2: Tagging**


**We could add a comment to our case about improving our process through tagging.** 

How could we have used tagging better? 

What are the benefits of improved tagging?

Ultimately, tagging is about labeling items so they can be easily found at another time. This allows you to find and organize items easier.



## Creating a Common Language

**Remember how...**

- We added a tag when we created our case at the beginning of qualification? 
- We made up our initial tag on the spot. We didn't use any specific catalog of terms or labeling best practices. 
- We didn't really think about how we were going to use it before we decided on our tag.

**Going forward...**

- We can use MITRE ATT&ACK tags. Many people use them as a common language to describe threats.



## Common Language: Benefits

If you have commonality across how you describe something, this leads to better understanding.    

We should use a common language when tagging because it allows for:

- **Sharing of Intelligence:** For example, we could communicate with other energy providers about the threats we're seeing, share indicators of compromise, and be better informed. 
- **Easy Searching & Reassigning of Cases**
    - Think about this: If you come across something you've never seen before, you can open the cases pane and click the filter button next to the name of the case. This then allows you to very quickly search for a tag.
    - After searching a tag, you may see other cases that seem related.
    - Instead of having to deal with the case yourself, you could reach out to the analyst on the related case. Since they're already looking into things, the case might even be reassigned to them.


# **Improvement #3: Playbooks**

**Another way we could have improved is by using a playbook.**

How can we take today's case, and make an actionable plan moving forward for similar situations?



## What are Playbooks at LogRhythm?

Playbooks answer the question: **"What do I do if XYZ happens?"** 

- Playbooks represent a way to store and manage standard procedures, including documentation of those procedures. Playbooks could be used for malware, phishing, or other processes such as unapproved software installations.     
- **They are instructions for what to do in a given situation.**
    
    - They provide a **series of steps** to help you respond to a situation, from discovery to mitigation. Some might start after discovery or not take you all the way through mitigation. It depends on your team. 
- There are existing playbooks that can be downloaded from LogRhythm, or you can write your own playbooks.


## Benefits

**Playbooks are helpful. Here's why:**

- You don't have to recall every action needed when you have them documented in a Playbook, only where to reference those actions. It allows you to shift the mental load from having to remember everything yourself to knowing where to look.  
    
- It allows us to document repeatable steps of what to do if this same situation occurs again.
- It helps assist us with consistency and the possible impacts of turnover.


## What would you do?

Imagine you were assigned to create a playbook for new hires who will encounter situations similar to the case we just handled.

What steps would you include?



