
Port
88    Kerveros
111   RPCbind
139   Smb
389   ldap
3268  ldap
593   ncacn_http
2049 nlockmgr
3389 ms-wbt-server
5985 http
9389 mc-nmf

Port 111 aka RPCbind
This stuff is related to API's i think so as of now

```
rpcdump.py RAZ0RBLACK/HAVEN-DC@10.10.56.115
anonymous
```
Output
```
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

Password:
[*] Retrieving endpoint list from 10.10.56.115
Protocol: N/A 
Provider: N/A 
UUID    : E40F7B57-7A25-4CD3-A135-7F7D3DF9D16B v1.0 Network Connection Broker server endpoint
Bindings: 
          ncalrpc:[LRPC-d10e4d3c66f7b774cc]
          ncalrpc:[OLEF5B081BD12A18D3F442CB6B8D435]
          ncalrpc:[LRPC-1e7a208d9549124d6e]
          ncalrpc:[LRPC-1260b6e2b361f675fd]

Protocol: N/A 
Provider: N/A 
UUID    : 0D3E2735-CEA0-4ECC-A9E2-41A2D81AED4E v1.0 
Bindings: 
          ncalrpc:[LRPC-b13c41de0857ad4c5b]
          ncacn_np:\\HAVEN-DC[\pipe\LSM_API_service]
          ncalrpc:[LSMApi]
          ncalrpc:[LRPC-e66b3ec9d90695d3ba]
          ncalrpc:[actkernel]
          ncalrpc:[umpo]

```

```
rpcinfo 10.10.56.115
```

From the data this is the info we were able to know that we can access's this services
```
(root㉿kali)-[~/TryHackMe/Raz0rBlack]
└─# rpcinfo -p 10.10.56.115
   program vers proto   port  service
    100000    2   udp    111  portmapper
    100000    3   udp    111  portmapper
    100000    4   udp    111  portmapper
    100000    2   tcp    111  portmapper
    100000    3   tcp    111  portmapper
    100000    4   tcp    111  portmapper
    100003    2   tcp   2049  nfs
    100003    3   tcp   2049  nfs
    100003    2   udp   2049  nfs
    100003    3   udp   2049  nfs
    100003    4   tcp   2049  nfs
    100005    1   tcp   2049  mountd
    100005    2   tcp   2049  mountd
    100005    3   tcp   2049  mountd
    100005    1   udp   2049  mountd
    100005    2   udp   2049  mountd
    100005    3   udp   2049  mountd
    100021    1   tcp   2049  nlockmgr
    100021    2   tcp   2049  nlockmgr
    100021    3   tcp   2049  nlockmgr
    100021    4   tcp   2049  nlockmgr
    100021    1   udp   2049  nlockmgr
    100021    2   udp   2049  nlockmgr
    100021    3   udp   2049  nlockmgr
    100021    4   udp   2049  nlockmgr
    100024    1   tcp   2049  status
    100024    1   udp   2049  status

```

Got the RPC terminal through Anonymous login
```
rpcclient -U "" -N <ip>
```
![[Pasted image 20230918175435.png]]

We got access denied 
![[Pasted image 20230918175635.png]]


┌──(root㉿kali)-[~/TryHackMe/Raz0rBlack]
└─# showmount -e 10.10.56.115
Export list for 10.10.56.115:
/users (everyone)

mount -t nfs [-o vers=2] 10.10.56.115:users mount -o nolock
┌──(root㉿kali)-[~/TryHackMe/Raz0rBlack]
└─# mount -t nfs -o vers=2 10.10.56.115:users mount -o nolock
mount.nfs: requested NFS version or transport protocol is not supported for /root/TryHackMe/Raz0rBlack/mount

mount -t nfs [-o vers=2] 10.10.56.115:/users /mount -o nolock

I think there's no luck here as well

MSFconsole
 5  auxiliary/scanner/nfs/nfsmount                                                     normal     No     NFS Mount Scanner

![[Pasted image 20230918181552.png]]

I think it's a dead end for now will what is /users after enumerating other ports well

Will enumerate port 3389
```
nmap --script "rdp-enum-encryption or rdp-vuln-ms12-020 or rdp-ntlm-info" -p 3389 -T4 10.10.56.159
```

```
└─# nmap --script "rdp-enum-encryption or rdp-vuln-ms12-020 or rdp-ntlm-info" -p 3389 -T4 10.10.56.159
Starting Nmap 7.94 ( https://nmap.org ) at 2023-09-19 05:27 EDT
Nmap scan report for 10.10.56.159
Host is up (0.16s latency).

PORT     STATE SERVICE
3389/tcp open  ms-wbt-server
| rdp-enum-encryption: 
|   Security layer
|     CredSSP (NLA): SUCCESS
|     CredSSP with Early User Auth: SUCCESS
|_    RDSTLS: SUCCESS
| rdp-ntlm-info: 
|   Target_Name: RAZ0RBLACK
|   NetBIOS_Domain_Name: RAZ0RBLACK
|   NetBIOS_Computer_Name: HAVEN-DC
|   DNS_Domain_Name: raz0rblack.thm
|   DNS_Computer_Name: HAVEN-DC.raz0rblack.thm
|   Product_Version: 10.0.17763
|_  System_Time: 2023-09-19T09:27:18+00:00

Nmap done: 1 IP address (1 host up) scanned in 4.32 seconds
```

![[Pasted image 20230919150043.png]]

