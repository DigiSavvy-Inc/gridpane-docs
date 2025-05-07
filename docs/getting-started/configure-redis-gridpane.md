# Configure Redis | GridPane

# Configure Redis

 

8 min read 

### Table of Contents

 

## Introduction

Redis is a high-performance in-memory database. For WordPress purposes, it is primarily used as a key-value store for object caching.

This can provide a major performance boost as once a query has been processed by your database, the result is cached in RAM and the database won’t have to process that request again. This results in much faster response times and less server processing once a query has been processed.

Below are the available GP-CLI to help you adjust your Redis configuration if you wish to do so.

If you’re running servers with 1-2GB of RAM and you’re receiving an alert about it hitting its allowed memory limit in Monit:

REDIS MEM_HIGH Warning!REDIS has been using a lot of RAM for at least the last 10 minutes… it is exceeding the Monit allowed threshold!

The section below will allow you to increase your RAM allocation, but you may wish to consider a larger server.

 

## Before You Begin: Single Redis vs Split Redis

Before you begin, head over to your account’s Servers page and open Monit for your server. Depending on when you provisioned your server, you will see either a single “redis-server” as shown in the image below:

Or you’ll see two Redis processes named “redis-page” and “redis-object“:

The commands for configuring Redis on your server will depend on which server type you’re configuring.

 

## Adjusting Redis Maxmemory

GridPane provisioned servers come with ~10% of total memory allocated to Redis. But there may be times when you’d like to increase/decrease this value to better suit your needs.

### redis-server Commands

Unit: MBDefault value: 10% of your servers RAM. E.g. 2GB RAM = [approx] 200MB etc

```
gp stack redis -max-memory $integer_max_memory
```

The below example will set the redis maxmemory to 300MB:

```
gp stack redis -maxmemory 300
```

### redis-page and redis-object Commands

```
gp stack redis-page -maxmemory $integer_max_memory
```

```
gp stack redis-object -maxmemory $integer_max_memory
```

For example:

```
gp stack redis-page -maxmemory 300
```

```
gp stack redis-object -maxmemory 300
```

back to top ▲

 

## Redis Maxmemory Eviction Policy

Redis is allocated a specific amount of memory that it’s not allowed to exceed. If it hits this limit, it will begin to evict “keys” in order to not exceed it.

### What is a “key”?

Almost every piece of data stored in Redis is assigned a key/value pair. The “key” is a name assigned to a piece of data. When you evict a key, you remove it’s associated data from Redis memory.

Available values:

### Redis-server commands

Default value: allkeys-lfu

```
gp stack redis -maxmemory-policy $key_eviction_policy $optional_max_memory
```

The following example will set the maxmemory policy to allkeys-lfu:

```
gp stack redis -maxmemory-policy allkeys-lru
```

The following example will set the maxmemory policy to allkeys-lfu and the maxmemory allocation to 300MB:

```
gp stack redis -maxmemory-policy allkeys-lru 300MB
```

### redis-page and redis-object Commands

```
gp stack redis-page -maxmemory-policy $key_eviction_policy $optional_max_memory
```

```
gp stack redis-object -maxmemory-policy $key_eviction_policy $optional_max_memory
```

For example:

```
gp stack redis-page -maxmemory-policy allkeys-lru 300
```

```
gp stack redis-object -maxmemory-policy allkeys-lru 300
```

back to top ▲

 

## Redis Persistence

With this GP-CLI you have the option to enable persistence and disable persistence.

Enabling persistence takes all data stored in RAM and writes it to disk. This use RBD persistence as well as what’s known as Append Only File (AOF) persistence. This mode provides much better durability, writing to disk on a per-second basis by default.

Disabling persistence uses RBD persistence only, and keeps all data stored in RAM and, which is more performant. However, when a server is shut down the entire Keystore is wiped, so all Redis caching data is cleared and needs to be rebuilt.

Default value: Enabled

### Enable

```
gp stack redis -enable-persistence
```

### Disable

```
gp stack redis -disable-persistence
```

back to top ▲

 

## Troubleshooting the REDIS MEM_HIGH Warning notification

This notification can sometimes be quite persistent when it occurs. Fortunately, this is nothing to worry about.

Your websites will use as much Redis as they are able to (storing pages, database queries, etc to the cache), and then Redis will automatically self-regulate and flush itself down to its limit when it goes over.

Monit, your server monitoring tool, will pick it up when it goes over its threshold and send this warning. Usually, you’ll find it will resolve itself it short order.

### Option 1. Increase Maxmemory

There are a couple of solutions on how you can choose to handle this. The first is to follow the Adjusting Redis Maxmemory settings above. We don’t recommend that you increase this above 25% of the total available RAM, but this can be a quick and easy solution, especially if you have a website where the database size exceeds the current Redis Maxmemory limit.

### Option 2. Prevent Notifications

If continual notifications are becoming a problem, you can make an adjustment to your Redis settings that will prevent Monit from sending this specific warning notification.

To do this, we need to increase the Monit threshold above the maxmemory by enough so that it won’t trigger the warning message. We can do this using our GP-CLI, which you can learn more about here:

Configure Monit Service Management and Notifications with GP-CLI

##### Step 1: View the Redis Monit Configuration File

```
cat /etc/monit/conf.d/redis
```

Here you will see the following:

```
# gridpane monit redis v2check process redis-serverwith pidfile "/var/run/redis/redis-server.pid"start program = "/usr/sbin/service redis-server start"stop program = "/usr/sbin/service redis-server stop"if cpu usage > 120% for 10 cycles then exec "/usr/local/bin/gpmonitor REDIS CPU_HOT warning" AND repeat every 10 cyclesif cpu usage > 160% for 5 cycles then exec "/usr/local/bin/gpmonitor REDIS CPU_RESTART error"if totalmem > 907 MB for 5 cycles then exec "/usr/local/bin/gpmonitor REDIS MEM_HIGH warning" AND repeat every 5 cyclesif totalmem > 1207 MB for 10 cycles then exec "/usr/local/bin/gpmonitor REDIS MEM_RESTART error"if failed host 127.0.0.1 port 6379 then restartif children > 255 for 5 cycles then restartif 5 restarts within 5 cycles then exec "/usr/local/bin/gpmonitor REDIS FAILED error" AND repeat every 1 cycles
```

This is from a 4GB RAM server. To prevent this notification, we could adjust this setting from “907 Mb” to “2000 Mb“. This increase will ensure that any memory spikes don’t trigger the warning message before Redis automatically flushes excess storage.

### Single Redis Commands

Run the following command, switching out “2000” for the number that makes sense for you:

```
gpmonit redis -mem-high-mb 2000
```

### Split Redis Commands

You can adjust Redis page and object notifications individually with these commands:

```
gpmonit redis-page -mem-high-mb 2000
```

```
gpmonit redis-object -mem-high-mb 2000
```

 

## Further Reading

You can learn more about Redis configurations in the redis.conf file. To view it, copy and paste the following command:

```
cat /etc/redis/redis.conf
```

You can learn more about configuring Redis Monit Notifications here:

Configure Monit Service Management and Notifications with GP-CLI #Redis

 

## Legacy

Please use the GP-CLI above to configure Redis. The below is not recommended for GridPane, but may be useful for none GridPane servers.

### Edit The Redis Configuration

Open the Redis configuration file with this command:

```
nano /etc/redis/redis.conf
```

Scroll down to where it says MEMORY MANAGEMENT. The setting you are looking for is maxmemory.

```
################## MEMORY MANAGEMENT ##################
# Set a memory usage limit to the specified amount of bytes.# When the memory limit is reached Redis will try to remove keys# according to the eviction policy selected (see maxmemory-policy).## If Redis can't remove keys according to the policy, or if the policy is# set to 'noeviction', Redis will start to reply with errors to commands# that would use more memory, like SET, LPUSH, and so on, and will continue# to reply to read-only commands like GET.## This option is usually useful when using Redis as an LRU or LFU cache, or to# set a hard memory limit for an instance (using the 'noeviction' policy).## WARNING: If you have replicas attached to an instance with maxmemory on,# the size of the output buffers needed to feed the replicas are subtracted# from the used memory count, so that network problems / resyncs will# not trigger a loop where keys are evicted, and in turn the output# buffer of replicas is full with DELs of keys evicted triggering the deletion# of more keys, and so forth until the database is completely emptied.## In short... if you have replicas attached it is suggested that you set a lower# limit for maxmemory so that there is some free RAM on the system for replica# output buffers (but this is not needed if the policy is 'noeviction').#maxmemory 503mb
```

Once you’ve changed the maxmemory value, Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

### Reload The Redis Configuration

Use this command to reload the Redis configuration:

```
systemctl restart redis.service
```

### Check Your Work (optional)

If you want to see what Redis sees, you can run info memory from the Redis prompt. To get into the Redis prompt, type the following command:

```
redis-cli
```

Enter info memory at the prompt and hit Enter.

```
root@rooty:~# redis-cli127.0.0.1:6379> info memory# Memoryused_memory:6529328used_memory_human:6.23Mused_memory_rss:12427264used_memory_rss_human:11.85Mused_memory_peak:7362536used_memory_peak_human:7.02Mused_memory_peak_perc:88.68%used_memory_overhead:875358used_memory_startup:791320used_memory_dataset:5653970used_memory_dataset_perc:98.54%allocator_allocated:6949344allocator_active:7491584allocator_resident:14700544total_system_memory:4136083456total_system_memory_human:3.85Gused_memory_lua:37888used_memory_lua_human:37.00Kused_memory_scripts:0used_memory_scripts_human:0Bnumber_of_cached_scripts:0maxmemory:527433728maxmemory_human:503.00Mmaxmemory_policy:allkeys-lfuallocator_frag_ratio:1.08allocator_frag_bytes:542240allocator_rss_ratio:1.96allocator_rss_bytes:7208960rss_overhead_ratio:0.85rss_overhead_bytes:-2273280mem_fragmentation_ratio:1.92mem_fragmentation_bytes:5938960mem_not_counted_for_evict:0mem_replication_backlog:0mem_clients_slaves:0mem_clients_normal:49694mem_aof_buffer:0mem_allocator:jemalloc-5.1.0active_defrag_running:0lazyfree_pending_objects:0
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

