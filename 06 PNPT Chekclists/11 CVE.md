
Print Night Mare
https://github.com/calebstewart/CVE-2021-1675


## [Manual checks](https://github.com/xbufu/PrintNightmareCheck#manual-checks)

### Check if `Print Spooler` service is running
```powershell
# Using WMIC
wmic service list brief | findstr "Spool"

# Using PowerShell
Get-Service "Print Spooler"
```

### Check latest security patches
```powershell
Get-HotFix -Description "Security*" | Sort-Object -Property InstalledOn
```


