# Utilizing Block Storage through Digital Ocean, Vultr, etc | GridPane

# Utilizing Block Storage through Digital Ocean, Vultr, etc

 

2 min read 

Third-Party Software Notice
Warning: this guide is unsupported, everything in this article is at your own risk. Please ensure you have full backups. Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

We routinely get asked about using lock Block Storage through some of our native providers. At this moment, we don’t officially support it, but you can definitely add it manually and leverage some of the neat benefits that Block Storage provides.

You may need to adapt this on a provider by provider basis, but we’re using Digital Ocean as a template. One piece of advice we’d give, if you’re wanting to use this for sites, I’d recommend doing it on a brand new server that has no customer sites on it. The example below is for backups, but you could use the same process for web files or other things.

When you first create the Block Storage volume, DO would show something like:

```
# Create a mount point for your volume:$ mkdir -p /mnt/volumename
```

```
# Mount your volume at the newly-created mount point:$ mount -o discard,defaults,noatime /dev/disk/by-id/scsi-0DO_Volume_volumename /mnt/volumename
```

```
# Change fstab so the volume will be mounted after a reboot$ echo '/dev/disk/by-id/scsi-0DO_Volume_volumename /mnt/volumename ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```

From the above you’ll gain the real disk ID. Then you’d want to use the below commands. The below is an example of if you’d want to move our local backups over to block storage.

```
mv /opt/gridpane/backups /opt/gridpane/backups-altmkdir /opt/gridpane/backupsmount -o discard,defaults,noatime /dev/disk/by-id/scsi-0DO_Volume_volumename /opt/gridpane/backupsecho '/dev/disk/by-id/scsi-0DO_Volume_volumename /opt/gridpane/backups ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstabcp -pr /opt/gridpane/backups-alt/* /opt/gridpane/backups/
```

If all looks good, do:

```
rm -r /opt/gridpane/backups-alt
```

All sites (WordPress core files) are stored at /var/www/site.url/htdocs . You could either move all of /var/www/ to block storage, or you could just move wp-content/uploads, or wherever the files you are wanting to move are. If you go super granular with this, you might have to add extra mounts to the same storage. You could also add multiple blocks. We’re not sure if Linode or DO has limits, but we are sure there is a limit somewhere down the road. We’d recommend probably no more than four volumes.

If you have questions about this guide, please feel free to post in the community forum.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

