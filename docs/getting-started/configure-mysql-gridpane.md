# Configure MySQL | GridPane

# Configure MySQL

 

12 min read 

## Index

Configuration file and using these commands

MySQL Variables

▲

 

## Configuration File and using these commands

These changes are recorded in the mysqld.cnf which resides at the following filepath:

```
/etc/mysql/mysql.conf.d/mysqld.cnf
```

Settings configured in a mysqld.cnf are global by nature and impact each WordPress site using the MySQL server. If you have sites which have drastically different demands of the Database then it might be best to separate such sites into servers that contain sites sharing similar profiles. This way you can more effectively tune MySQL as per the demands of your WordPress sites.

GP-CLI Stack MySQL commands do not reload configuratoins immediately, this is because MySQL needs to stop and restart to load in new configurations. Therefore if you are going to make several changes it might be best to chain commands together and use a reload/restart command.

For example:

```
gp stack mysql -max-connections 100 &&  
gp stack mysql -innodb-buffer-pool-size 2048 && 
gp stack mysql -innodb-buffer-pool-instances 2 && 
gp mysql restart
```

 

## MySQL Server Variables

▲

### Set the binary log (binlog) expiration period.

Sets the binary log expiration period in seconds. After their expiration period ends, binary log files can be automatically removed. Possible removals happen at startup and when the binary log is flushed.

Variable: binlog_expire_logs_secondsUnit: SecondsDefault value: 2592000Accepted values: 0-4294967295

```
gp stack mysql -binlog-expire-logs-seconds {accepted.value}
```

Example:

```
gp stack mysql -binlog-expire-logs-seconds 86400
```

back to top ▲

▲

 

### Set the lock mode to use for generating auto-increment values

The lock mode to use for generating auto-increment values. Permissible values are 0, 1, or 2, for traditional, consecutive, or interleaved, respectively.

Variable: innodb_autoinc_lock_modeDefault value: 1Accepted values: 0 (traditional), 1 (consecutive), 2 (interleaved)

```
gp stack mysql -innodb-autoinc-lock-mode {accepted.value}
```

Example:

```
gp stack mysql -innodb-autoinc-lock-mode 2
```

back to top ▲

▲

 

### Set the number of innodb buffer pool instances

The number of regions that the InnoDB buffer pool is divided into. For systems with buffer pools in the multi-gigabyte range, dividing the buffer pool into separate instances can improve concurrency, by reducing contention as different threads read and write to cached pages.

This option only takes effect when setting innodb_buffer_pool_size to 1GB or more. The total buffer pool size is divided among all the buffer pools. For best efficiency, specify a combination of innodb_buffer_pool_instances and innodb_buffer_pool_size so that each buffer pool instance is at least 1GB.

Variable: innodb_buffer_pool_instancesUnit: GBDefault value: 8 (or 1 if innodb_buffer_pool_size < 1GB)Accepted values: 1 – 64

```
gp stack mysql -innodb-buffer-pool-instances {accepted.value}
```

Example:

```
gp stack mysql -innodb-buffer-pool-instances 2
```

back to top ▲

▲

 

### Set the size of the innodb buffer pool instances

The size in bytes of the buffer pool, the memory area where InnoDB caches table and index data. The maximum value is 18446744073709551615 (264-1) bytes on 64-bit systems. When the size of the buffer pool is greater than 1GB, setting innodb_buffer_pool_instances to a value greater than 1 can improve the scalability on a busy server.

Variable: innodb_buffer_pool_sizeUnit: MBDefault value:  64 MB if the total RAM is less than 1200MB at the time the server is provisioned, or 128MB if more.Accepted values: 5 – 18446744073709

```
gp stack mysql -innodb-buffer-pool-size {accepted.value}
```

Example:

```
gp stack mysql -innodb-buffer-pool-size 2048
```

back to top ▲

 

### Controls the balance between strict ACID compliance and higher performance

Controls the balance between strict ACID compliance for commit operations and higher performance that is possible when commit-related I/O operations are rearranged and done in batches.

Variable: innodb_flush_log_at_trx_commitDefault value: 1Accepted values: 0, 1, 2

```
gp stack mysql -innodb-flush-log-at-trx-commit {accepted.value}
```

Example:

```
gp stack mysql -innodb-flush-log-at-trx-commit 2
```

back to top ▲

▲

 

### Define the method used to flush data to InnoDB data files and log files

Defines the method used to flush data to InnoDB data files and log files, which can affect I/O throughput.

Variable: innodb_flush_methodDefault value: O_DIRECTAccepted values: fsync, O_DSYNC, littlesync, nosync, O_DIRECT, O_DIRECT_NO_FSYNC

```
gp stack mysql -innodb-flush-method {accepted.value}
```

Example:

```
gp stack mysql -innodb-flush-method O_DSYNC
```

back to top ▲

▲

 

### Define the standard number of IOPS available to InnoDB background tasks

The innodb_io_capacity variable defines the number of I/O operations per second (IOPS) available to InnoDB background tasks, such as flushing pages from the buffer pool and merging data from the change buffer.

Variable: innodb_io_capacityDefault value: 1000Accepted values: 1 – 1.8446744e+19

```
gp stack mysql -innodb-io-capacity {accepted.value}
```

Example:

```
gp stack mysql -innodb-io-capacity 500
```

back to top ▲

▲

 

### Define the maximum number of IOPS available to InnoDB background tasks

If flushing activity falls behind, InnoDB can flush more aggressively, at a higher rate of I/O operations per second (IOPS) than defined by the innodb_io_capacity variable. The innodb_io_capacity_max variable defines a maximum number of IOPS performed by InnoDB background tasks in such situations.

Variable: innodb_io_capacity_maxDefault value: 2000Accepted values: 1 – 1.8446744e+19

```
gp stack mysql -innodb-io-capacity-max {accepted.value}
```

Example:

```
gp stack mysql -innodb-io-capacity-max 2500
```

back to top ▲

▲

 

### Define the size of each log file in a log group

The size in bytes of each log file in a log group. The combined size of log files (innodb_log_file_size * innodb_log_files_in_group) cannot exceed a maximum value that is slightly less than 512GB. A pair of 255 GB log files, for example, approaches the limit but does not exceed it.

Variable: innodb_log_file_sizeUnit: MBDefault value: 100Accepted values: 512GB / innodb_log_files_in_group

```
gp stack mysql -innodb-log-file-size {accepted.value}
```

Example:

```
gp stack mysql -innodb-log-file-size 256
```

back to top ▲

▲

 

### Define the minimum buffer size used to scan indexes and joins that do not use indexes

The minimum size of the buffer that is used for plain index scans, range index scans, and joins that do not use indexes and thus perform full table scans. Normally, the best way to get fast joins is to add indexes. Increase the value of join_buffer_size to get a faster full join when adding indexes is not possible. One join buffer is allocated for each full join between two tables. For a complex join between several tables for which indexes are not used, multiple join buffers might be necessary.

Variable: join_buffer_sizeUnit: KBDefault value: 256Accepted values: 128 – 18446744073709547520

```
gp stack mysql -join-buffer-size {accepted.value}
```

Example:

```
gp stack mysql -join-buffer-size 512
```

back to top ▲

▲

 

### Define the minimum time to be recognised as a long query for slow query logging

If a query takes longer than this many seconds, the server increments the slow_queries status variable. If the slow query log is enabled, the query is logged to the slow query log file. This value is measured in real time, not CPU time, so a query that is under the threshold on a lightly loaded system might be above the threshold on a heavily loaded one. The minimum and default values of long_query_time are 0 and 10, respectively.

This setting requires slow_query_log to be enabled to do anything.

Variable: long_query_timeUnit: SecondsDefault value: 0 (but disabled)Accepted values: 0+

```
gp stack mysql -long-query-time {accepted.value}
```

Example:

```
gp stack mysql -long-query-time 512
```

back to top ▲

▲

 

### Define the maximum size of a binlog file under normal circumstances*

If a write to the binary log causes the current log file size to exceed the value of this variable, the server rotates the binary logs (closes the current file and opens the next one). The minimum value is 4096 bytes. The maximum value is 1GB. Encrypted binary log files have an additional 512-byte header, which is included in max_binlog_size.

*A transaction is written in one chunk to the binary log, so it is never split between several binary logs. Therefore, if you have big transactions, you might see binary log files larger than max_binlog_size.

Variable: max_binlog_sizeUnit: MBDefault value: 100Accepted values: 1 – 1000

```
gp stack mysql -max-binlog-size {accepted.value}
```

Example:

```
gp stack mysql -max-binlog-size 512
```

back to top ▲

▲

 

### Define the maximum number of simultaneous client connections to the MySQL Server

The maximum permitted number of simultaneous client connections to the MySQL server.

Variable: max_connectionsUnit: IntegerDefault value: 200Accepted values: 1 – 100000

```
gp stack mysql -max-connections {accepted.value}
```

Example:

```
gp stack mysql -max-connections 151
```

back to top ▲

▲

 

### Enable/Disable the slow query log.

Whether the slow query log is enabled. The value can be 0 (or OFF) to disable the log or 1 (or ON) to enable the log. This function will also enable the long_query_time of 0 seconds, you may wish to also adjust this variable.

Variable: slow_query_logUnit: BooleanDefault value: 0 (OFF)Accepted values: 0 (OFF), 1 (ON)

```
gp stack mysql -slow-query-log {accepted.value}
```

Example:

```
gp stack mysql -slow-query-log 1
```

MySQL slow query log output can be viewed in the following log:

```
/var/log/mysql/slow.log
```

back to top ▲

▲

 

### Determine how the server handles threads for client connections

Determines how the server handles threads for client connections. In addition to threads for client connections, this also applies to certain internal server threads, such as Galera slave threads.

Variable: thread_handlingDefault value: one-thread-per-connectionAccepted values: one-thread-per-connection, no-threads, pool-of-threads

```
gp stack mysql -thread-handling {accepted.value}
```

Example:

```
gp stack mysql -thread-handling pool-of-threads
```

back to top ▲

▲

 

### Manage the thread pool high priority scheduling mode

This variable is used to provide more fine-grained control over high priority scheduling either globally or per connection.

Variable: thread_pool_high_prio_modeDefault value: transactionsAccepted values: transactions, statements, none

```
gp stack mysql -thread-pool-high-prio-mode {accepted.value}
```

Example:

```
gp stack mysql -thread-pool-high-prio-mode statements
```

This variable is inactive unless thread_handling is set to pool-of-threads

back to top ▲

▲

 

### Assign the number of tickets in the high priority queue policy

This variable controls the high priority queue policy. Each new connection is assigned this many tickets to enter the high priority queue. Setting this variable to 0 disables the high priority queue.

Variable: thread_pool_high_prio_ticketsUnit: IntegerDefault value: 4294967295

```
gp stack mysql -thread-pool-high-prio-tickets {accepted.value}
```

Example:

```
gp stack mysql -thread-pool-high-prio-tickets statements
```

This variable is inactive unless thread_handling is set to pool-of-threads

back to top ▲

▲

 

### Limit the time an idle thread should wait before exiting

This variable can be used to limit the time an idle thread should wait before exiting.

Variable: thread_pool_idle_timeoutUnit: SecondsDefault value: 60

```
gp stack mysql -thread-pool-idle-timeout {accepted.value}
```

Example:

```
gp stack mysql -thread-pool-idle-timeout 30
```

This variable is inactive unless thread_handling is set to pool-of-threads

back to top ▲

▲

 

### Limit the maximum number of threads in a pool

This variable can be used to limit the maximum number of threads in the pool. Once this number is reached no new threads will be created.

Variable: thread_pool_max_threadsUnit: IntegerPercona max value: 100000MariaDB max value: 65536Default value: Max value above

```
gp stack mysql -thread-pool-max-threads {accepted.value}
```

Example:

```
gp stack mysql -thread-pool-max-threads 50000
```

This variable is inactive unless thread_handling is set to pool-of-threads

back to top ▲

▲

 

### Define the number of threads that can use the CPU at the same time

This variable can be used to define the number of threads that can use the CPU at the same time.

Variable: thread_pool_sizeUnit: IntegerDefault value: Number of CPU Cores

```
gp stack mysql -thread-pool-size {accepted.value}
```

Example:

```
gp stack mysql -thread-pool-size 4
```

This variable is inactive unless thread_handling is set to pool-of-threads

back to top ▲

▲

 

### Define the number of milliseconds before a running thread is considered stalled

The number of milliseconds before a running thread is considered stalled. When this limit is reached thread pool will wake up or create another thread. This is being used to prevent a long-running query from monopolizing the pool.

Variable: thread_pool_stall_limitUnit: MillisecondsDefault value: 500

```
gp stack mysql -thread-pool-stall-limit {accepted.value}
```

Example:

```
gp stack mysql -thread-pool-stall-limit 1000
```

This variable is inactive unless thread_handling is set to pool-of-threads

back to top ▲

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

