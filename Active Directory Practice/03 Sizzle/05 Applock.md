
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
Clone the respository
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

I tried installing Elite but it's deprecated Temporarily 