
Instead of capturing the hashes we can simply relay that hashes to gain access

Couple of Requirement 
- [ ] SMB signing must be disabled or not enforced on the target
- [ ] Relayed user credentials must be admin on machine (i.e. Local admin)

We couldn't relay the attack to ourself which means that fcastle can't send request to itself and relay to himself.

We have fcastle has local admin on his machine and Peter Parker machine

Identify host without SMB signing
```
nmap --script=smb2-security-mode.nse -p445 <ip_address>
```
![[Pasted image 20240120122918.png]]



Some configuration changes to the responder
SMB and HTTP should be off so that is not captured but relayed
```

```

