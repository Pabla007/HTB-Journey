
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

