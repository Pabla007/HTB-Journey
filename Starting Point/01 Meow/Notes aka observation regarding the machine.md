- Here we have connected the machine with vpn using openvpn
- One the connection was established we run the ICMP echo request aka ping request to check if the machine is ruining or not.
		`ping <ip address> -c 4`
- Then run the Nmap scan
		 `nmap -T4 -p- -A <ip address>`
- Established the connection on port 23 where telnet was running.
		 `telnet <ip address> port 23`
We can log into telnet with black password with root username
				`ls`
				`cat flag.txt`
Hurray we have successfully cached the flag.

