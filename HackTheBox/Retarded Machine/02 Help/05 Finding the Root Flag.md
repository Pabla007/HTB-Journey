I simply hosted the linpeas.sh file and download it using the wget command as curl was not installed
![[Pasted image 20230811220541.png]]

As ./ didn't worked i used bash linpeas.sh
![[Pasted image 20230811221132.png]]

Linux version 4.4.0-116-generic (buildd@lgw01-amd64-021) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.9) ) #140-Ubuntu SMP Mon Feb 12 21:23:04 UTC 2018

![[Pasted image 20230811221422.png]]

I simply wget the file as i was not able to copy and paste it
![[Pasted image 20230813113615.png]]

We finally able to run the exploit.c and able to privilege access from normal user to root
gcc exploit.c -o exploit
![[Pasted image 20230813114221.png]]

root@help:/root# wc -c root.txt 
33 root.txt
root@help:/root# cat root.txt 
047505c53f2077f3686924138e914692
