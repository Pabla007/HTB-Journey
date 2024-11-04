

I am going to give my PNPT exam and this is the details i got please make a checklist and give me the methodology so that i can safe my time. Please 
keep in mind that we are following the NIST SP800-115.pdf so make the checklist accordingly

Exam : 
OSINT 
Might be having RCE vulnerability
External - Web application Vulnerability 
Internal - Windows/Linux Privilege Escalation , Active Directory


Don't develop a CTF find otherwise you will fail (clearly mentioned)

PNPT exam by TCM security

I have watched all the videos and blogs and this is what I have found till now.


From 1st Video:
There is an external site that they will provide outside of the lab
environment (i.e. where we should start our initial recon)

1st Day
Compromise: 12:12 PM
Shell: 1:19 PM
Internal Shell: 4:10 PM
Third Shell: 5:00 PM
Fourth Shell: 4:60 PM

2nd Day
Domain Admin: 9:00 AM


From Blog
Exam pattern

OSINT Client Site
External Pentest : 10.10.155.0/24
Internal Pentest : 10.10.10.0/24


Not in Scope:
DOS attacks
Phishing / Social Engineering Attacks
Attacks against the [Redacted] website or any public facing infrastructure

PT to full compromise of TPM domain Controller.
Professionally Written Report
15 Minute Debrief

Any brute force attempts can be done using Fast track wordlist.
Any password cracking attempts can be done with rockyou.txt

Checklist
Lab Access
Scope/Goals
OSINT
External 
Nmap
Internal
x.x.x.x
x.x.x.x
x.x.x.x
x.x.x.x
Screenshots
Credentials / users
Secretsdump
Writeup Steps
Findings
Commands
Other



From 2nd Video:
- develop a methodology how u r going to attack every box
- Take tips and how to solve a box from Siren
- Pivoting and Enumerating AD


From 3rd Video:
I found the course material was more than sufficient enough to pass the exam. Despite this, 
I did use the following additional resources to practice for the exam but, 
I will reiterate that the course material is enough to pass.


- Make sure you know different pivoting tools and techniques for the exam.
- If you get stuck, think about what you identified/recovered and how it can be used. Don’t overthink it!
- You will run out of ideas before you run out of time!



My Research

Exam is not same as the course material it requires 
60-70 recon than exploitation.
Osint part is very small.... it will be really quick

More focus on reconnaissance

We have to move laterally from 5 machines.
All machines are vulnerable.
Focus on AD tools and methodology.

In PNPT we have to do recon and find the way to the 1st machine.

Looks for other's mistake and Ur Common Sense
Don't skipping a step in my methodology and missing obvious steps
Like Mis-configurations

If you are in the CTF mindset, you are likely going to fail.




 Key To Pass the Exam
Enumerate -> Enumerate -> Enumerate -> Enumerate
If Stuck Check your Methodology make sure we enumerate everything 
OSINT
Gather Publically Facing Information for the users.

External Compromise
Compromise the external assest

Pivot internally

Move laterally , Escalate Privileges or Complete Domain Compromise

Basic Enumeration , basic exploits and use what you found.


Time is your Enemy
 Make sure you know different pivoting tools and techniques for the exam.
- If you get stuck, think about what you identified/recovered and how it can be used. Don’t overthink it!
- You will run out of ideas before you run out of time!



