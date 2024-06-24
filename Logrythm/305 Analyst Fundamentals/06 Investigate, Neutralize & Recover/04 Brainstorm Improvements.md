
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


## **Improvement #4: SmartResponse**

**Another way we could improve our process in the future is to include and use SmartResponse.** This allows us to perform preventative actions when threatening activity is detected. In other words, it's something you want to happen automatically in response to something else.



## What is a SmartResponse in the LogRhythm SIEM?

**A SmartResponse:**

- Is a prebuilt script, set up by an Administrator in the Client Console, that executes an action you can run through LogRhythm. 
- Can be set up to be executed automatically or manually (requiring someone's approval).


## Examples

In this situation, we could have used a SmartResponse to:

- **Run a virus scan.** Rather than calling IT Ops to initiate a malware scan, we could have just clicked on a SmartResponse to start it. That could have saved 5-10 minutes.  
- **Add Adam to a List.** We could add Adam to a watch list.
- **Check for Windows updates**. Checking for updates would allow us to check for any security holes that may exist.
- **Run SupportAssist.** On Dell computers, we could run support assist to see if we have any hardware driver updates that need to happen.
- **Quarantine Adam's Device.** We didn't end up needing to do this; however, this would have been a nice option to have, just in case.


## Benefits

SmartResponses are helpful because:

- They make an Analyst's life easier.
- They cut down on response time.
- They help ensure we're doing the same things consistently and to the same standard.
- They allow us to take action from the LogRhythm console without having to log into any other systems, tools, or resources.  
    - For example, SmartResponse can be added to playbooks. You can do everything from one given spot. You don't have to navigate to different resources.
    - It helps eliminate confusion, extra work, navigating to a different spot, and missing steps. 
    - Having all of your actions and playbooks in one given location helps ensure that we'll get it right.



# **Improvement #5: Contextualized Searches**

**We can set up and use Contextualized Searches.**  These provide information about a host, port, or user in a log or event.


## What is Contextualized Search in LogRhythm?

Contextualized Searches:

- Give the Analyst the ability to query a third-party data source by integrating third-party systems and commonly used security tools within the LogRhythm system.
- Are all about integrating other resources into LogRhythm so that you don't have to look elsewhere. It's a script that performs a task, such as "go to Google and Google X."


## Examples

In the situation we just faced, we could integrate: 

- **VirusTotal, Mitre Att&ck, or other security sites** which are used to look up malicious content or false positives. A lot of Analysts use these. In fact, I use VirusTotal in my everyday life! 
- **Shodan, Ipinfo, nslookup, Google** - In this case, we had an unknown IP address, which we later realized was Dropbox. We could have set the contextualize option for the metadata field of IP address: known host, host name, and just asked "what is this IP address" to one of these sites. Contextual search would allow us to find out actually what that IP address is registered to, and then very quickly bring that information back into the case.


## Benefits

Contextualized Search is helpful because it allows you to:

- **Access all of your tools from one place**  
    For example, instead of having to open up a new browser tab to Google something, you could just Google it directly from within LogRhythm. You could simply open the inspector window, click on view detail, and run a contextualized search.
- **Quickly and seamlessly see what other people and systems are saying**  
    It's a quick way to see directly from the Web Console what other people and systems are saying about the information you found within your LogRhythm console. This could help speed up your case metrics.
- **Adds Detail & Context**  
    Whether it's a specialist search engine or simply you looking something up, contextualization quickly gives the Analyst additional information.
- **Build the Story**  
    This is what an Analyst is doing. They're adding flavor and color to what they already know. They're basically taking a word (a piece of data) and then building it out into a sentence, a paragraph, a chapter, and then into a book. This is done by adding layers of surrounding information. In the end, they've built out the details of the book and then can retell the story.


