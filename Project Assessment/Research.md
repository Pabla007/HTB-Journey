All hospitals have a few things in common, including they all endorsed the new healthcare law that was passed. You’ve learned from your legal team that your hospital endorsed the law as well.

They’ve noticed that the attackers are consistently targeting Windows systems that contain centralized log files and backups
They are also taking advantage of an unpatched Windows vulnerability to execute the attack.

The IP address for your main log server is the IP address of your Azure virtual machine. You store all of your logs and backup logs in your data center on-site. Full backups are conducted once on the first of every month. Though you always change the default passwords, you haven’t enforced strong passwords consistently with your users.


You attempt to log into your log analysis tool, but that’s no longer accessible.
Your security leader has declared this a critical security incident.
Action: Outline, the next steps you recommend taking in the report template.






Impact Considerations
 
a)            What is the indicator of compromise?
The control systems used to monitor patient is being compromised which is a sign that suggest something suspicious is happening.Those suspicious signs are called indicators of compromise (IoC). When an IoC is confirmed, it typically gets labeled an incident.

b)           What is the potential impact of the incident?
After doing more research come to know that the Hospital is under Ransome ware attack which as impacted the patients as lives are at risk cuz doctors are not able to see the patients information so that they can treat them.
 
c)            Name of system being targeted, the operating system, and the IP address. (use lab environment machine)
Name of the System :
OS : Microsoft Windows 10 1809 - 2004
IP address : 10.0.0.4


 
Consider and answer the following questions on triage:
 
a)            Is the incident confirmed? Or an indicator of compromise that’s not yet verified?
Monday 09:00 AM : 1st Update 
At this point the IOC was not being verified and the search to do was started asap the information was passed to the cybersecurity team.

Monday 01:00 PM : 3rd Update
The incident was confirmed by the staff memeber of hospital X as the monitoring system was being compromised.

b)           Is the incident contained already or still in progress? 
Still in progress
 
c)            Is the response urgent? 
Yes it's critical as doctors can't treat the patients cuz they don't have the patients information. 
 
d)           Will any response alert the attacker and if so, do we care? 
Yes if the price is not paied than the attacker would get the alert. But we don't care about that as we already know how they operate and do the things they shouldn't
 
e)            What type of incident is this? Example: virus, worm, intrusion
Ransomware is a type of malware from cryptovirology that threatens to publish the victim's personal data or permanently block access to it unless a ransom is paid off.


    
Is safety or human life at immediate risk? - the IR team should ensure their own survival and survival of the staff as a priority.
As all the system are being locked out so the patients life is at risk cuz system will get back soon from the updated that are taken monthly though there will be loss of data.
But loss of data is not that much risk cuz life will be lost if system are not come online soon so yes it's an immediate risk.



Which recommended changes should the IR team make to prevent the occurrence from happening again or infecting other systems. Upon approval changes are to be implemented. Action examples are included below however, you should develop recommendations tailored to the attack at hand.

Re-install the affected system(s) from scratch and restore data from backups if necessary. Preserve evidence before doing this. 
Before formating and start the things will like to preserve the evidenec of the mail that was being clicked and the system image has been saved so that we have do a detailed research what when wrong and hospital X got compromised even after getting a head-ups.

Make users change passwords if passwords may have been sniffed. 
As the FIN4 is know for getting the password so it recommend for the user to use strong password using password manager as well as strong password policy should be carried out. 

Ensure the system has been hardened by turning off or uninstalling unused services. 
Should make outbound rules for port 80 and 443 so that cyber attack like ransomware could not take place from next time. As well as see if any unwanted services or app was installed by the group.
 
Ensure the system is fully patched. 
Rescanning is an important step: Cuz it could fix one issue by changing a configuration, and when ran the scan again, that old issue was fixed but five new ones poped up and it almost became a game of whack-a-mole.

Be sure real time virus protection and intrusion detection is running. 


Review response and update policies—plan and take preventative steps so the intrusion can't happen again. Which updates do you recommend and why?

Consider whether an additional policy or technology could have prevented the intrusion ?
Strong Password Policy and the time for update should be taken weekly rather than montly. Cuz in this type of attack the data is being compromised and will be lost.So to keep the loss at minimum this should be followed.

Was the incident response appropriate? How could it be improved? 
Yes the Incident response is appropriate as already got the heads-up and after knowing about the enemy (i.e. FIN4). It's an advantage to know the the group works and what's there motto. 
Though there is no silver bullet in cybersecurity which could save us. But we have taken every step and each phase from vulnerability scanning to penetate testing the passwords. As well as good through plan for incident response but i am all ear's if anyone want to add something.

Were the incident-response procedures detailed and did they cover the entire situation? How can they be improved? 
Yes and no both the incident response can be more detail for an ransomware attack as it is already on rise from couple of years. So rather than having a response plan for malware incident it would be good to have ransomware instead. And yes some steps were very detailed as well no doubt in that (i.e. like traige questions etc..)

What changes can be made to prevent a re-infection?
Employee's ignorance is also a threat to security so staff should be trained and should give a head-ups so that we could save the organization.
Password as very very poor it should be dealt with strong password asap

What lessons have been learned from this experience?
If any new compliance is being endorsed than legal team should contact the Cybersecurity team and give an head-up about the siutation so if there's any vulnerabiltiy that we should be one that should discover it first and set the controls and take necessary steps.
People are the weakest point in cyber attack (i.e. Weak password has been set by staff and clicked the phising mail)  


