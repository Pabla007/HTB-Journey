
```
Remote collection configurations will vary, depending on the log source type that is being collected:
```


## Windows Event Logs

As discussed, using a service account with appropriate permissions, will allow a System Monitor Agent installed on Windows to communicate and pull logs from another Windows host. Generally, an agent will be configured to collect Event Viewer logs, but it can also collect logs from specified directories within Windows (flat files).

![[Pasted image 20240515114934.png | 400]]

