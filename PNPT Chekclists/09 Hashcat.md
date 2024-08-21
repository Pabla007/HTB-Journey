
1st Check the type of Hash-cat
```
hashcat --help | grep NTLM
```

```
hashcat --help | grep Kerberos
```


```
.\hashcat.exe -m 18200 -D 2 .\hashes4.txt .\rockyou.txt -O
```


another alternative is Google Colab


<hr>

But we have to check the version of NTML for that we have a command

```
hashcat --help | grep NTLM
```
![[Pasted image 20240120120911.png]]

or we can search directly on hashCat wiki

NTLMv2 it cracks a little bit slower than NTLMv1



<hr>



Let's crack the hash
```
hashcat --help | grep Kerberos
```
![[Pasted image 20231117125521.png]]
as the type was not mentioned so i decided to test everytype till we don't get the error for mismatch

```
.\hashcat.exe -m 18200 -D 2 .\hashes4.txt .\rockyou.txt -O
```

