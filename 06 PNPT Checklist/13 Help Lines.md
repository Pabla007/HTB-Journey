
Cut the hashes 
```
cat hashes.out | grep ::: | awk -F: '{print $4}'
```

```
cat hashes.out | grep ::: | awk -F: '{print $1":"$4}'
```


https://ippsec.rocks/?#