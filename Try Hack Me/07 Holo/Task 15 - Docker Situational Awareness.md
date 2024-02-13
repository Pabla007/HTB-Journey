
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

