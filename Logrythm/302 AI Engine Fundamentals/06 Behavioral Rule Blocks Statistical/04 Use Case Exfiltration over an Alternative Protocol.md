This Statistical Rule Use Case is looking for exfiltration over a protocol not used in the initial attack, such as FTP, SMTP, etc. 

This rule would look for protocols or applications from an Origin Host and group by Impacted Host for 2 or more protocols:

i.e. normally infrastructure is setup to have dedicated functions 
i.e. a Web Server serves information only on port 443 or a mail server only serves or delivers email on port 25 (SMTP) or 587 if it is secure SMTP.

![[Pasted image 20240609095732.png]]

## Resources

Further reading and reference:

- [(opens in a new tab)](https://attack.mitre.org/techniques/T1135/)MITRE ATT&CK Technique T1048 Exfiltration over an alternative Protocol: https://attack.mitre.org/techniques/T1048/ 
- Tools used for Egress and Ingress testing: [https://github.com/FortyNorthSecurity/Egress-Assess(opens in a new tab)](https://github.com/FortyNorthSecurity/Egress-Assess)
- Exfiltration tool using steganography and DNS queries: [https://github.com/TryCatchHCF/PacketWhisper(opens in a new tab)](https://github.com/TryCatchHCF/PacketWhisper)
- DropFlop use Dropbox as a Command and Control and Data Exfiltration tool: [https://github.com/pauln23/DropFlop](https://github.com/pauln23/DropFlop)


