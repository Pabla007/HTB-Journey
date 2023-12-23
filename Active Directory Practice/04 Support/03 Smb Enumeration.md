
```
smbclient \\\\10.10.11.174\\support-tools -U 'anonymous'
```
![[Pasted image 20231121143858.png]]

I think we have to enumerate more and see what we can find on userinfro.exe.zip
![[Pasted image 20231121145636.png]]

```
b03f5f7f11d50a3a
a0Nv32PTwgYjzg9
8j5TbmvPd3e7WhtWWyuPsyO76
Y+U193Earmando%LDAP

```
![[Pasted image 20231121145745.png]]

```
<UserName>k__BackingField<LastName>k__BackingField<FirstName>k__BackingField<
TextkeyGetExecutingAssemblyLdapQueryqueryDirectoryEntryentrya0Nv32PTwgYjzg9/8j5TbmvPd3e7WhtWWyuPsyO76/Y+U193Earmando%LDAP://support.htbsupport\ldapa[-] At least one of -first or -last is required.(givenName=)      (sn=(givenName=
                                                                       )(sn=))/[*] LDAP query to use: sAMAccountNameQ[-] No users identified with that query.[+] Found  results:       [-] Exception: +[*] Getting data for sAMAccountName=pwdLastSetlastLogongivenNamesn        mail+[-] Unable to locate s. Please try the find command to get the user's username.-First Name:           -Last Name:            -Contact:              -Last Password Change:   findFind a user user9Get information about a userUserInfo.exe
```

I think now we have to enumerate the .exe file that we got which looks sus to me
UserInfo.exe let's see we can run it as we got from the above error to give some sore of name in order to get it working but i can't run donet in linux
![[Pasted image 20231121152816.png]]

https://www.geeksforgeeks.org/how-to-install-net-on-linux/
https://www.wikihow.com/Can-Linux-Run-Exe

![[Pasted image 20231121153902.png]]

We are not able to run dotnet so another options is given in the walkthrough will try to run the in order to decompile the exe file
ILSpy is the **open-source .** **NET assembly browser and decompiler**

```
wget https://github.com/icsharpcode/AvaloniaILSpy/releases/download/v7.2-rc/Linux.x64.Release.zip
```

```
unzip Linux.x64.Release.zip
```

```
unzip ILSpy-linux-x64-Release.zip
```

```
./ILSpy
```
![[Pasted image 20231121162103.png]]
Will get something like this

Simply load the file
![[Pasted image 20231121162222.png]]

After Enumerating got an encrypted password
Encrypted Password
```
0Nv32PTwgYjzg9/8j5TbmvPd3e7WhtWWyuPsyO76/Y+U193E
```
Key
```
armando
```


Statics analysis only possible if we install wine or dotnet install

So instead of running the java or writing python code we have to use cyberchef and set the encoding carefully
It's decoded in base 64 : from base 64
Xor with key armando : that is utf 8
Xor with key 223 : that is decimal
![[Pasted image 20231122130521.png]]

![[Pasted image 20231121163251.png]]

We have simply convert the code into python another way is to run the .exe file and list than in wireshark
```

// UserInfo.Services.Protected
using System;
using System.Text;

internal class Protected
{
        private static string enc_password = "0Nv32PTwgYjzg9/8j5TbmvPd3e7WhtWWyuPsyO76/Y+U193E";

        private static byte[] key = Encoding.ASCII.GetBytes("armando");

        public static string getPassword()
        {
                byte[] array = Convert.FromBase64String(enc_password);
                byte[] array2 = array;
                for (int i = 0; i < array.Length; i++)
                {
                        array2[i] = (byte)((uint)(array[i] ^ key[i % key.Length]) ^ 0xDFu);
                }
                return Encoding.Default.GetString(array2);
        }
}

```

With little error i was able to install wine
https://www.sysnettechsolutions.com/en/install-wine-kali-linux/
![[Pasted image 20231121181755.png]]

```
wine UserInfo.exe -v find
[-] At least one of -first or -last is required.
```

```
wine UserInfo.exe -v find -first "support"
[*] LDAP query to use: (givenName=support)
[-] Exception: No Such Object
```

