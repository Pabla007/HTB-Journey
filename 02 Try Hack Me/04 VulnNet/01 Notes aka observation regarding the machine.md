So the ports we should look into are 
139/445 smb
![[Pasted image 20230915185755.png]]

464/tcp     kpasswd5?
6379/tcp    redis         Redis key-value store 2.8.2402
![[Pasted image 20230915190110.png]]
```
[+] 10.10.14.47:6379      - Found redis with INFO command: $1791\x0d\x0a# Server\x0d\x0aredis_version:2.8.2402\x0d\x0aredis_git_sha1:00000000\x0d\x0aredis_git_dirty:0\x0d\x0aredis_build_id:b2a45a9622ff23b7\x0d\x0aredis_mode:standalone\x0d\x0aos:Windows  \x0d\x0aarch_bits:64\x0d\x0amultiplexing_api:winsock_IOCP\x0d\x0aprocess_id:1884\x0d\x0arun_id:18f985c54f3cbd00ed88a98752f02ced238987af\x0d\x0atcp_port:6379\x0d\x0auptime_in_seconds:1601\x0d\x0auptime_in_days:0\x0d\x0ahz:10\x0d\x0alru_clock:285794\x0d\x0aconfig_file:\x0d\x0a\x0d\x0a# Clients\x0d\x0aconnected_clients:1\x0d\x0aclient_longest_output_list:0\x0d\x0aclient_biggest_input_buf:0\x0d\x0ablocked_clients:0\x0d\x0a\x0d\x0a# Memory\x0d\x0aused_memory:953208\x0d\x0aused_memory_human:930.87K\x0d\x0aused_memory_rss:919640\x0d\x0aused_memory_peak:953208\x0d\x0aused_memory_peak_human:930.87K\x0d\x0aused_memory_lua:36864\x0d\x0amem_fragmentation_ratio:0.96\x0d\x0amem_allocator:dlmalloc-2.8\x0d\x0a\x0d\x0a# Persistence\x0d\x0aloading:0\x0d\x0ardb_changes_since_last_save:0\x0d\x0ardb_bgsave_in_progress:0\x0d\x0ardb_last_save_time:1694783009\x0d\x0ardb_last_bgsave_status:ok\x0d\x0ardb_last_bgsave_time_sec:-1\x0d\x0ardb_current_bgsave_time_sec:-1\x0d\x0aaof_enabled:0\x0d\x0aaof_rewrite_in_progress:0\x0d\x0aaof_rewrite_scheduled:0\x0d\x0aaof_last_rewrite_time_sec:-1\x0d\x0aaof_current_rewrite_time_sec:-1\x0d\x0aaof_last_bgrewrite_status:ok\x0d\x0aaof_last_write_status:ok\x0d\x0a\x0d\x0a# Stats\x0d\x0atotal_connections_received:4\x0d\x0atotal_commands_processed:3\x0d\x0ainstantaneous_ops_per_sec:0\x0d\x0atotal_net_input_bytes:56\x0d\x0atotal_net_output_bytes:0\x0d\x0ainstantaneous_input_kbps:0.00\x0d\x0ainstantaneous_output_kbps:0.00\x0d\x0arejected_connections:0\x0d\x0async_full:0\x0d\x0async_partial_ok:0\x0d\x0async_partial_err:0\x0d\x0aexpired_keys:0\x0d\x0aevicted_keys:0\x0d\x0akeyspace_hits:0\x0d\x0akeyspace_misses:0\x0d\x0apubsub_channels:0\x0d\x0apubsub_patterns:0\x0d\x0alatest_fork_usec:0\x0d\x0a\x0d\x0a# Replication\x0d\x0arole:master\x0d\x0aconnected_slaves:0\x0d\x0amaster_repl_offset:0\x0d\x0arepl_backlog_active:0\x0d\x0arepl_backlog_size:1048576\x0d\x0arepl_backlog_first_byte_offset:0\x0d\x0arepl_backlog_histlen:0\x0d\x0a\x0d\x0a# CPU\x0d\x0aused_cpu_sys:0.23\x0d\x0aused_cpu_user:0.58\x0d\x0aused_cpu_sys_children:0.00\x0d\x0aused_cpu_user_children:0.00\x0d\x0a\x0d\x0a# Keyspace

```


9389/tcp   mc-nmf        .NET Message Framing

