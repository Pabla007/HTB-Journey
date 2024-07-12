
Let's see if i have understood the concept of Pivoting correctly or there are some loop holes which i need to work on.

SO what i am going to do it i will not use any software like
Chisel / Sshuttle / Socat etc....

And try to do the configuration of Double pivoting using Proxychains and SSH.


### The Layout

Machines in Wreath lab are as follows:

| IP              | Hostname         | Notes           |
| --------------- | ---------------- | --------------- |
| 10.50.88.33     | `attack`         | My box          |
| 192.168.122.172 | `jumpbox1.local` | First jump box  |
| 192.168.122.212 | `jumpbox2.local` | Second jump box |
| 192.168.122.181 | `destbox.local`  | Final machine   |