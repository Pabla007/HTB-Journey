
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
