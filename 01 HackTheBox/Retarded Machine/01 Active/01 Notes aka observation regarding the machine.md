- Here we have connected the machine with vpn using openvpn
- One the connection was established we run the ICMP echo request aka ping request to check if the machine is ruining or not.
		`ping <ip address> -c 4`
- Then run the Nmap scan

Final thoughts we simply target the SMB here in the Active Directory as we don't have any user id and passwords. How could be compromise the Active Directory.

As the we can see the Windows Server is 2008 and there is attack or loop hole in the Cpassword aka GPP which we could abuse in the SMB

So will login as anonymous in the smb and download the content from the replication share 
from there we got the cpassword and user name from the GROUP.xml file.

To see if the the user is administrator will use psexec and got to know that user is low level.
moreover will use GetUserSPN as we already have the service ticket (i.e. Kerberosating)

We got the -] Kerberos SessionError: KRB_AP_ERR_SKEW(Clock skew too great) error and rectify it setting our machine and active htb time similar using

```
timedatectl set-ntp true
timedatectl set-ntp false
and then retry ntpdate <domain ip address>
````

Hopefully we got the kerberosting ticket and using hashcat we got the password and username

After than we run the psexec and volla we were able to connect.
to see the content of the .txt file in windows file we use **more** and **type** command

It is not a piece of cake as we have to do a lot of reconnaissance before really start digging the hole to find the loop hole.