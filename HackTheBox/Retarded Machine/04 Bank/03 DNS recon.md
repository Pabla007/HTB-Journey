dnsrecon -r 127.0.0.0/24 -n bank.htb -d blah 
![[Pasted image 20230813133927.png]]
![[Pasted image 20230813134808.png]]

Will see if the zone transfer is enables and we can do it or not
And yes we were able to do it.
dig axfr bank.htb @10.10.10.29
![[Pasted image 20230814111426.png]]

We will add the nameserver to the /etc/resolve.conf file
![[Pasted image 20230814111750.png]]

