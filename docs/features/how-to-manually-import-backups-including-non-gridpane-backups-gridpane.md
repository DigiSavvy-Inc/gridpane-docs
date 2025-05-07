# How to Manually Import Backups (Including Non-GridPane Backups) | GridPane

# How to Manually Import Backups (Including Non-GridPane Backups)

 

4 min read 

## Introduction

This tutorial details how to manually import a GridPane V2 backup that you’ve previously downloaded, or a non-GridPane backup that is properly configured to work with our system (details included here too). This requires connecting to your server over SFTP to upload your backup and then using your website customizer inside your GridPane account to run the import.

### Table of Contents

 

## Backup Configuration

If the backup you’re importing is a GridPane backup, you can skip this section as your backup is already correctly configured.

### Non-GridPane Backups

Our backups system requires your backup to be configured as a compressed tarball. This is an compressed archive file in the TAR (Tape Archive) format, similar to a zipped file.

The structure requires your database and then your htdocs directory containing your WordPress files.

 

 

### Important

Please make sure there is no wp-config.php file inside your htdocs folder.

### mydumper Database Export

The structure within the tarball needs to be:

```
htdocs
database-{epoch}
```

For example, the database directory might be called (you can replace the number with anything):

```
database-1664208000
```

### Creating your tar.gz file

A program like PeaZip can handle this for you. PeaZip is open source and works on Windows, Mac, and Linux.

If you’ve collected your files together and zipped them, PeaZip and other similar programs can also convert .zip files into tar.gz files.

On Mac and Linux, you can also create a tar.gz file via your terminal by navigating to the folder where your htdocs and database are and running:

```
tar -czvf youbackupname.tar.gz .
```

 

## Uploading Your Backup

To restore a backup that you originally exported via SFTP, you can do this by first uploading to a directory called restores in /var/www/site.url.

This location is also detailed inside the backups tab inside your website customizer as well:

The backup file needs to by .tar.gz format.

To upload your backup, connect to your server via SFTP and add the tar.gz to your server. You can learn how to connect to your servers via SFTP in these articles:

Once uploaded, click “No Archives Found” to check for your upload. Then select your backup and hit the Restore Now button.

 

## Import Options

Regular websites, Full Git configured sites, Hybrid Git configured sites, and Multitenancy sites all have their own import options. How your site is configured will determine what our application shows you. We’ll walk through each of them below.

To choose your backup, open up your website customizer and go to Backups > Restore:

Under Restore from Export, select your backup from the dropdown, and click Restore Now.

 

### Regular (Non-Git) Websites

When importing a regular website, you’ll have the following options:

 

### Full Git Webites

When restoring backups to a Full Git configured website, you will have the following 5 options:

 

### Hybrid Git Websites

When restoring backups to Hybrid Git configured sites, you have the following 5 options (the first 2 differ from Git Full):

The first 2 options won’t replace the files in your Git repo.

 

### Multitenancy Git Websites

When restoring backups to websites on your multitenancy servers, you will have the following options:

These options differ from regular Full Git configured websites as these can be reverted to regular WordPress sites whenever required, which isn’t possible on a multitenancy server.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

