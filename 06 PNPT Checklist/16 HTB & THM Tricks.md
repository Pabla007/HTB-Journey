
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





# Sauna:

#### **Things to Look For**:

1. **Services and Protocols**:
    
    - LDAP (389) and Kerberos (88) for AD attacks.
    - SMB (445) for share enumeration and lateral movement.
    - Web services for potential vulnerabilities and misconfigurations.
2. **Hashes and Credentials**:
    
    - Use tools like `GetNPUsers.py` and `kerbrute` to extract Kerberos hashes.
    - Crack credentials with `Hashcat` and use them for WinRM or SMB access.
3. **Privilege Escalation**:
    
    - Enumerate AD relationships with **BloodHound**.
    - Perform DCSync attacks with `secretsdump.py` to extract domain hashes.


ASREPRoasting
DCSync Attack

Enumeration:
Nmap 
Ldap
SMB
Web

Foothold:
HashCat 
WinRM

Privilege Escalation:
Bloodhound
DCSync 


Sauna:

Enumeration:
Nmap 
enum4linux
kerbrute 
GetNPUsers.py
HashCat

Foothold:
HashCat 
WinRM -> Evil-winrm

Privilege Escalation:
Bloodhound
DCSync 
secretsdump.py



# Active:

- **Weak Credentials**:
    
    - Default or embedded credentials in GPP files.
    - Reuse of credentials across services.
- **AD Exploitation**:
    
    - Enumerate SPNs and other Kerberos-related vulnerabilities.
    - Misconfigured permissions or roles for privilege escalation.
- **SMB Shares**:
    
    - Look for sensitive files like GPP configurations or password stores.
- **Service-Specific Vulnerabilities**:
    
    - Focus on LDAP, SMB, and Kerberos for AD environments.


SMB enumeration techniques

Enumeration:
Nmap
SMB

Foothold:
GPP
Authenticated Enumeration

Privilege Escalation:
Kerberoasting


GetUserSPNs.py active.htb/svc_tgs:'GPPstillStandingStrong2k18' -dc-ip 10.10.10.100 -request

