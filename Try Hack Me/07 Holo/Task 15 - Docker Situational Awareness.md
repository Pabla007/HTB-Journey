
Upload the image in the of the docker to get an idea of the container - Application and Environment.

Situation Awareness

Containers have network capabilities and their own file storage: Namespaces Cgroups Overlays

But we are interested in Namespaces here cuz they segregate system resources such as processes , files and memory away from namespaces.

Let's POC by comparing the number of processes there are in Docker container that is running a web server versus the host.

Containers allow environment variables to be provided from the host operating system by the use of a .dockerenv file. This file is located in the "/" directory and would exist on a container -even if no environment variables were provided.

to check if docker env is there or not this is the command
```
cd / && ls -lah
```
![[Pasted image 20240211103153.png | 500]]

```
cd /proc/1
```
![[Pasted image 20240211103411.png | 300]]

```
cat cgroup
```
![[Pasted image 20240211103345.png]]

Cgroups are used by containerization software such as LXC or Docker. pwd cat cgroup

<hr>

In the checklist check the tools and things installed like basic things netcat is installed or prepare a nc folder of precompiled binaries to save the time.

Living of the LAND This is the 2nd time i have heard about this term after the wreath network. A Critical part of situational awareness is identifying network and host information. So that can be done via port scanning and network tooling. (i.e. Netcat and statically compiled binaries)

1st Method | Port scanning | Bash

Take SS of this command ls -la /dev/

/dev/tcp/ipaddr/port

2nd Method | Port Scanning | Python

python script using sockets

3rd Method | Netcat | Assuming that it's installed on the system

Simply do Enumeration maunally / using scripts

As we already the server we are attacking is a web server : SQL or database on the backened. Keep in mind that these server are hevily secured from outside traffic but but but internally the story is different and often very insecure as we can read the configuration files.

Web Servers require db_connect.php to connect PHP and SQL. Can't read it entirely but can gain some info from it easily.

So to access the database we need a binary of the database access tool used. Database will be MySQL but it will change from server to server as well as the location may also vary.

mysql -u <username> -p -h 127.0.0.1 -u is for username -p parameter however it does not take an argument. -h parameter to access remote databases.
