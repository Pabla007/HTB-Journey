
### The Advanced Intelligence Engine (AIE) is an advanced analytics component.

AIE is what allows LogRhythm to **examine and** ****e**valuate logs in real-time** in order to detect whether sophisticated log activity with a negative impact is occurring in the environment.


![[Pasted image 20240606180532.png]]

LogRhythm has an **Alarms** feature, where activity contained within one log can generate an alarm or notification to be received by an Analyst. At times, this is all that is needed. 

AIE, however, does not carry this limitation – activity can span multiple logs of different types with varying metadata and timing. This provides increased capabilities to detect more complex log behavior.



##  Example of successive log activity that would be captured by an AIE Rule:

1. New User Created 
2. New User Account Enabled 
3. Account has been granted elevated privileges 
4. Account logged on 
5. User access sensitive files 
    1. Log: REALTIME FILEMON EVENT=READ OBJECT=F:\Finance\Projected Earnings\Q42014WWBookings.xlsx USER=SANDBOX\steven.jacobs PROCESS=EXCEL.EXE OFFSET=0 LENGTH=8192 SIZE=465248 DETAILS=lastaccess=8/03/2017 9:00:16 AM -0800 lastwrite=8/4/2017 9:36:44 PM -0800 create=9/25/2016 8:25:45 AM -0800 usersid=S-1-5-21-3198741196-3878509842-143179808-1118 pid=3376 Policy=FinanceDataFIM 
6. A user uploads something to Dropbox
    1. Log: 08 03 2017 02:08:02 198.151.100.12 <LOC4:DBUG> Aug 3 19:04:11 probe LogRhythmDpi: EVT:001 a0b1c2d3-e4f5-a6b7-c8d9-e0f1a2b3c4d5:00 203.0.113.12,198.151.100.11,49209,80,e0:db:55:20:dc:ac,00:50:56:a7:56:1d,6,887,620/620,0/0,5/5,1478743448,1478743451,3/3,dname=203.0.113.13,command=PUT,version=1.1,object=Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.71 Safari/537.36,url=/,process=http://www.dropbox.com/ 
7. Logs off 
8. Account deleted


