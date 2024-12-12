
Now I will make different attack plans based on the box but it was clearly written that will get fail if we went with this strategy.


# Forest:
#### **Things to Look For**:

1. **Ports and Services**:
    
    - LDAP (389) and SMB (445) for AD enumeration.
    - RDP (3389) for potential remote access.
2. **AD Enumeration**:
    
    - Kerberos attacks (ASREPRoasting, Kerberoasting).
    - Domain trusts and privilege relationships with BloodHound.
3. **Credentials**:
    
    - Always check for hashes or passwords in dumped data.
    - Look for misconfigurations in permissions (`WriteDACL` or `WriteOwner`).
4. **Foothold and Escalation**:
    
    - Use PowerShell tools like PowerView for post-compromise enumeration.
    - Escalate using credentials and lateral movement (e.g., PsExec).



ASREPRoasting
Enumeration with Bloodhound
DCSync Attack

ldapsearch -h <ip_Address> -p 389 -x -b "dc=htb,dc=local"

Enumeration:
Nmap 
Ldap

Foothold:
GetNPUsers.py
HashCat 

1st way Privilege Escalation:
Bloodhound
Exchange Windows Permission -> WriteDacl
PowerView
Secretsdump/Psexec


2nd way Privilege Escalation:
Golden Ticket
Psexec / smb





