
### **Methodology (NIST SP 800-115 Based)**:

 - [ ] **Planning Phase:**
 - Confirm exam scope and define objectives: Full compromise of TPM Domain Controller.


 - [ ] **Discovery Phase (OSINT & External Recon):**
 - Gather OSINT (names, emails, subdomains) using tools like **theHarvester**, **Recon-ng**.
 - External scanning (Nmap, Gobuster, Nikto) for vulnerabilities.


 - [ ] **Vulnerability Identification:**
 - Identify potential exploits (e.g., RCE, misconfigurations) and escalate privileges.
 - Test external vulnerabilities, such as RCE or misconfigurations.


- [ ] **Exploitation Phase:**
- Obtain an initial shell via the compromised external asset.
- Escalate privileges using basic enumeration techniques (LinPEAS/WinPEAS, Metasploit).


- [ ] **Post-Exploitation & Lateral Movement:**
- Enumerate internal network assets, exploiting AD misconfigurations.
- Use **BloodHound**, **Mimikatz**, **Responder** to escalate privileges within AD.
- Pivot laterally across internal machines.


- [ ] **Domain Admin Compromise:**
- Gain Domain Admin credentials.
- Dump credentials from the Domain Controller.


- [ ] **Reporting Phase:**
-  Prepare a professional report with findings, methodology, and evidence (screenshots, exploited paths).
- Debrief with a 15-minute presentation.
