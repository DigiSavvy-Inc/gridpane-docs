# Fix: DigitalOcean Disk Space Failed to Resize Automatically | GridPane

# Fix: DigitalOcean Disk Space Failed to Resize Automatically

 

2 min read 

In almost all cases, DigitalOcean will automatically take of everything when you resize your servers. On reboot, the disk is resized and Monit automatically picks up these changes. Nothing is required from you.

One of the great things about them is that everything just works. They’ve done a great job of making everything seamless when you scale your servers up and down.

In very, very rare circumstances though, their process may fail, and you will need to fix things over the command line.

Their official documentation can be found here:https://docs.digitalocean.com/products/droplets/how-to/resize/

In it they state:

 

									In certain cases, a disk resize fails to resize the Droplet’s partition or filesystem. If you rerun `df -h` after a disk resize and the output is unchanged, this usually indicates a problem.								

## Resizing Disk Space Manually

Below we’ll follow DigitalOcean’s own guidance and examples from their documentation linked above.

### Step 1. Check your disk space

Run the following to confirm that the disk has not been resized correctly:

```
df -h
```

The output will look something like the following:

```
root@server:~# df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            979M     0  979M   0% /dev
tmpfs           199M   25M  3.2G   1% /run
/dev/vda1        25G   25G     0 100% /
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/loop0       33M   33M     0 100% /snap/snapd/12704
/dev/loop1       33M   33M     0 100% /snap/snapd/12398
/dev/loop2       62M   62M     0 100% /snap/core20/1026
/dev/loop3       43M   43M     0 100% /snap/certbot/1343
/dev/loop4       62M   62M     0 100% /snap/core20/1081
/dev/loop5       43M   43M     0 100% /snap/certbot/1280
/dev/vda15      105M  8.9M   96M   9% /boot/efi
tmpfs           199M     0  199M   0% /run/user/1003
tmpfs           199M     0  199M   0% /run/user/0
```

### Step 2. Verify available disk space

Use gdisk to get more information:

```
gdisk -l /dev/vda
```

The output looks like this:

```
GPT fdisk (gdisk) version 1.0.3
Partition table scan:
MBR: protective
BSD: not present
APM: not present
GPT: present
Found valid GPT with protective MBR; using GPT.
Disk /dev/vda: 104857600 sectors, 50.0 GiB
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): C1E73477-225B-4585-8BB5-C9291E473CE4
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 52428766
Partitions will be aligned on 2048-sector boundaries
Total free space is 2014 sectors (1007.0 KiB)
Number Start (sector) End (sector) Size Code Name
1 227328 52428766 24.9 GiB 8300
```

### Step 3. Resize Your Disk

To resize the partition, use the growpart command. /dev/vda is the name of the disk, separated by a space, and followed by the number of the partition to resize, 1.

```
growpart /dev/vda 1
```

Now resize the filesystem with:

```
resize2fs /dev/vda1
```

### CHECK YOUR WORK

To confirm that our new disk space is available, run the following command again:

```
df -h
```

You’ll now see the new amount on this line of the output:

```
/dev/sda1 50G 25G 25G 50% /
```

## Reload Monit

Now run the following to reload Monit and register the change:

```
monit reload
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

