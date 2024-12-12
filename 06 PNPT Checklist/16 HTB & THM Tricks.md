
Now I will make different attack plans based on the box but it was clearly written that will get fail if we went with this strategy.


## Forest:
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

