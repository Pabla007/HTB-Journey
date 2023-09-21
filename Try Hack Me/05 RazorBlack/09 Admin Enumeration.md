There is nothing in the desktop folder but there .xml in the user->lvetrova folder
![[Pasted image 20230920175408.png]]

And we got something 
![[Pasted image 20230920175506.png]]

```
xml file data
<Objs Version="1.1.0.1" xmlns="http://schemas.microsoft.com/powershell/2004/04">
  <Obj RefId="0">
    <TN RefId="0">
      <T>System.Management.Automation.PSCredential</T>
      <T>System.Object</T>
    </TN>
    <ToString>System.Management.Automation.PSCredential</ToString>
    <Props>
      <S N="UserName">Your Flag is here =&gt;</S>
      <SS N="Password">01000000d08c9ddf0115d1118c7a00c04fc297eb010000009db56a0543f441469fc81aadb02945d20000000002000000000003660000c000000010000000069a026f82c590fa867556fe4495ca870000000004800000a0000000100000003b5bf64299ad06afde3fc9d6efe72d35500000002828ad79f53f3f38ceb3d8a8c41179a54dc94cab7b17ba52d0b9fc62dfd4a205f2bba2688e8e67e5cbc6d6584496d107b4307469b95eb3fdfd855abe27334a5fe32a8b35a3a0b6424081e14dc387902414000000e6e36273726b3c093bbbb4e976392a874772576d</SS>
    </Props>
  </Obj>
</Objs>
```

It seems like a kerberos ticket to me and if u recall we even got the hash of it as well let's see where it all takes us

As i was wrong and the above data is  a xml representation of PSCredential Object.
https://jatinpurohit.wordpress.com/2020/04/08/decrypt-pscredential-object-password-and-its-applications/
https://systemweakness.com/powershell-credentials-for-pentesters-securestring-pscredentials-787263abf9d8

So how to decrypt it that the question that arises here
```
$Passwd = "01000000d08c9ddf0115d1118c7a00c04fc297eb010000009db56a0543f441469fc81aadb02945d20000000002000000000003660000c000000010000000069a026f82c590fa867556fe4495ca870000000004800000a0000000100000003b5bf64299ad06afde3fc9d6efe72d35500000002828ad79f53f3f38ceb3d8a8c41179a54dc94cab7b17ba52d0b9fc62dfd4a205f2bba2688e8e67e5cbc6d6584496d107b4307469b95eb3fdfd855abe27334a5fe32a8b35a3a0b6424081e14dc387902414000000e6e36273726b3c093bbbb4e976392a874772576d" | ConvertTo-SecureString
```

```
$cred = new-object System.Management.Automation.PSCredential("lvetrova", $Passwd)
```

$cred.GetNetworkCredential().password 
This command worked for me but without it was not giving me the password
```
$cred.GetNetworkCredential() | fl **
```
![[Pasted image 20230920182627.png]]

```
THM{694362e877adef0d85a92e6d17551fe4}
```

2nd way is simply where we can directly give the XML file 
```
$Credential = Import-Clixml -Path "lvetrova.xml"
$Credential.GetNetworkCredential().password
```

