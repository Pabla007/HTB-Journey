
```
The LogRhythm Threat Intelligence Service (TIS) collects threat feed data from supported vendors at scheduled intervals. It shows whether a metadata value is on a threat feed list.
```


1. Our Timeline search confirmed that Bob Smith opened a blocked email message, allowing a malware program installation that went on to delete files.
2. Our Timeline search also confirmed that Bob Smith was not logged into any other machines that day.
3. Our Wildcard search confirmed that the file deletions did not occur anywhere else other than Bob's machine.



**Also, I went ahead and took care of the latest step according to the Playbook:** 

- **"Request a desktop technician to unplug the network cable or shut off wireless."**
    - I just got off the phone with a technician. He's **taking Bob's machine off the network** right now in order to prevent deletions to network files or potential infection of other machines.



**Our next step:**

- **"Check the external IP Address against the Threat Intelligence feeds and add logs to the case as needed."**
    - I'll need you to take care of this for me. Here's how:
        - First, run a Threat Intelligence Service feed check for the Host (Origin) IP Address. We want to know if this IP shows up on any TIS feeds. If this IP is on a known "bad list," then the TIS feed should pick it up. After, add any information that does come up to the case notes.
        - While you are at it, can you also **check off that we got Bob's machine off the network?**



**What does this all mean?**

- To put it clearly, the Host Origin IP Address was picked up by the SANS Threat Intel List. with **Category: Attack**
- **Anything from this IP should be considered as a possible attack and definitely checked into.**
    - Not everything will be an attack, but SANS has evidence that traffic from this IP address has participated in some forms of attack(s) in the past.
- We now have a much clearer picture of this morning's events. We have successfully investigated the situation and neutralized the threat. I'm glad we had the Playbook to follow, which had us using SmartResponse to neutralize the threat early on in our process.

