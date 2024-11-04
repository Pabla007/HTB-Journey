We got an error when opened the site 
```
10.200.85.200
```
![[Pasted image 20231206142030.png]]


In real life we would perform a "footprinting" phase of the engagement at this point. This essentially involves finding as much public information about the target as possible and noting it down. You never know what could prove useful!
After adding the IP address in the host file we were able to view the site
```
10.200.85.200 thomaswreath.thm
```
![[Pasted image 20231206142204.png]]


We are not able to get the OS information from Nmap but able to get the OS info from Wappalyzer


Service Running : snet-sensor-mgmt 
Vulnerability : CVE-2019-15107

On searching the exploit i got a script to check if we can exploit it or not
https://github.com/MuirlandOracle/CVE-2019-15107
```
pip3 install -r requirements.txt
```
 It is, however, good practice to read through scripts before running them


```
https://thomaswreath.thm:10000/
```
![[Pasted image 20231206144238.png]]

Yup we were able to exploit it
![[Pasted image 20231206144625.png]]

![[Pasted image 20231206144859.png]]
![[Pasted image 20231206144922.png]]
Got a reverse shell with full access to have to write some code dumb shell to full aceess shell

```
python3 -c "__import__('pty').spawn('/bin/bash')"
stty -raw echo;fg
reset.

export TERM=xterm
```


Let's get the shadow file

```
cat /etc/shadow

root:$6$i9vT8tk3SoXXxK2P$HDIAwho9FOdd4QCecIJKwAwwh8Hwl.BdsbMOUAd3X/chSCvrmpfy.5lrLgnRVNq6/6g0PxK9VqSdy47/qKXad1::0:99999:7:::

twreath:$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg.::0:99999:7:::
```


```
ssh -i id_rsa root@thomaswreath.thm
chmod 600 id_rsa
```
chmod 600 ( rw------- )600 permissions means that **only the owner of the file has full read and write access to it**. Once a file permission is set to 600, no one else can access the file.
![[Pasted image 20231206150600.png]]

