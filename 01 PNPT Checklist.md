
### **Checklist:**

 **Pre-Engagement (Planning & Scope):**
 - [ ] Confirm scope
 - [ ] Ensure Lab Access and Exam rules understanding.
 - [ ] Define goals: 


 **OSINT:**
 - [ ] Gather public-facing information for users, subdomains, emails, and infrastructure.


**External Reconnaissance:**
- [ ] Start with **Nmap** scan of external assets (`10.10.155.0/24`)
- [ ] Look for open ports/services (RCE, web vulnerabilities).
- [ ] Exploit the external asset.


Internal Reconnaissance:
- [ ] **Initial Compromise:**
- [ ] Establish initial foothold and shell.
- [ ] Document all credentials/users found.

 - [ ] **Internal Reconnaissance (Post-Compromise):**
 - [ ] Scan internal network (`10.10.10.0/24`) from compromised host.
 - [ ] Look for AD misconfigurations, local exploits (Winpeas/Linpeas).
 - [ ] Enumerate for credentials (Secrets dump, Pass the Hash).

- [ ] **Lateral Movement & Privilege Escalation:**
- [ ] Pivot to internal hosts (Windows/Linux).
- [ ] Leverage AD tools (Bloodhound, Mimikatz) for AD enumeration.


 **Domain Compromise:**
  - [ ] Gain access to the **Domain Admin**.
  - [ ] Dump domain credentials.


**Documentation:**
- [ ] Take screenshots of all important steps.
- [ ] Ensure clear documentation for reporting.



![[Pasted image 20241021185325.png]]
![[Pasted image 20241021185345.png]]

