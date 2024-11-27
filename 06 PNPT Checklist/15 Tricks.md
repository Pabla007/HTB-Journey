
# Kill a process
How to kill a process running on particular port in Kali Linux ?_?
or
How to kill a process if it show's port already in use ?_?

Stack overflow:
fuser 8080/tcp will print you PID of process bound on that port.
And this fuser -k 8080/tcp will kill that process.

https://stackoverflow.com/questions/11583562/how-to-kill-a-process-running-on-particular-port-in-linux

