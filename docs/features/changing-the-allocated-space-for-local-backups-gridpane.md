# Changing the Allocated Space For Local Backups | GridPane

# Changing the Allocated Space For Local Backups

 

1 min read 

By default, we allocate 20% of server space for backups. If existing backups on the server exceed the allotted space, Borg will not create new backups or do anything else which requires a backup (staging pushes, clones, etc).

Why would that happen? Maybe you have a really large site. Maybe you take 24 manual backups on the 30 minute mark because you’re paranoid. Whatever the reason, 20% doesn’t always cut it. Fortunately, you can increase this value.

Accessing the Config File

The available space varies per server size, but you can change it with this command:

```
nano /opt/gridpane/backups/snapshots/config
```

Contents of the Config File

Once you’re in that file, it will look like this:

```
[repository]
version = 1
segments_per_dir = 1000
max_segment_size = 524288000
append_only = 0
storage_quota = 11000000000
additional_free_space = 0
id = (hidden for the KB, will show on your server)
key = (hidden for the KB, will show on your server)
```

The value you want to change is “storage_quota”. Save, write, and exit the file.

Bytes/GB Conversion

It’s in bytes and converts to GB like so:

1 GB = 10^9 bytes = 1,000,000,000 bytes

   10GB1000000000015GB1500000000020GB2000000000025GB2500000000030GB3000000000035GB3500000000040GB4000000000045GB4500000000050GB5000000000055GB5500000000060GB6000000000065GB6500000000070GB7000000000075GB75000000000 

## Further Reading

For further information about how backup systems work, the available options for configuring them, and for setting up remote backups (available on V2), please see the articles listed below.

### Strategy

Recommended Backup Strategy

### V2 Backup Documentation

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

