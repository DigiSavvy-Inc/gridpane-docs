# Useful Commands for Managing GridPane Servers | GridPane

# Useful Commands for Managing GridPane Servers

 

4 min read 

## Introduction

There are commands that can come in extremely useful for managing your GridPane servers. We use them ourselves, many of them daily, and knowing them should prove useful in your GridPane journey.

Let’s jump right in!

 

## Check Disk Space Per Website

First, navigate to the directory where your websites are stored with:

```
cd /var/www
```

And then run the following to sort them in order of file size:

```
du -h --max-depth=1 | sort -h
```

This is an extremely useful command. It will work for all directories on your server, not just your websites, but checking website disk space is likely the most common reason you’ll want to use it.

 

## Create a Magic Login Link

You can quickly and easily create a magic login link to login to any of your websites directly on your server. Normally, you can just SSO in, but if for some reason that’s not working, or you need to send a login link to a client (not really recommended), you can create one as outlined below.

Note: Links expire after 15 minutes or once they’ve been successfully used.

You can create one with GP-WP-CLI as follows:

```
gp wp site.url login create 1
```

Or with WP-CLI by navigating to your websites htdocs directory:

```
cd /var/www/site.url/htdocs
```

And running:

```
wp login create 1 --allow-root
```

 

## Backup a WordPress Database

Being able to quickly backup a WordPress database can come in handy when you’re about to perform any kind of clean up (better tested on staging first) or repair. You can create a backup with:

```
gp wp site.url db export /var/www/site.url/htdocs/name_of_backup.sql --all-tablespaces --add-drop-table
```

And restore a backup with:

```
gp wp site.url db import name_of_backup.sql
```

You can also check out this article for more database backup options: How to backup / export / import a WordPress database.

 

## Check and Repair a WordPress Database

These are handy commands if you’re seeing performance issues or database errors. You can check the health of a websites database with either GP-WP-CLI as follows:

```
gp wp site.url db check
```

And then, if necessary, repair it. Always back up your database before performing work on it. Copy and paste the following command to run the repair:

```
gp wp site.url db repair
```

 

## Backup a Website

If you’re working on a site inside your server and wish to make a backup, you can do so with the following command:

```
gpbup2 site.url -local-single-site
```

Note that the above command only works for V2 backups.

 

## Login to MySQL

If you need to login to MySQL directly on your server you can do so with the following GP-CLI command:

```
gp mysql login root
```

 

## Display your MySQL Password

If you’re working on your database remotely with a program such as MySQL Workbench, you can view your password with the following GP-CLI command:

```
gp mysql get-pass root
```

 

## Change a System User Password

If you need to change the password of one of your system users, or the default gridpane user, you can do so with the following:

```
passwd username
```

For example:

```
passwd mysystemusername
```

 

## Log Locations and How to View Them

You can view the last 300 lines of various logs in your site customizer modal, but if you need to view more, or would like to view specific logs in real-time. To view the logs list below you can use the cat command like so:

```
cat /path/to/example.log
```

Or you can view them in real time with the tail -f command:

```
tail -f /path/to/example.log
```

To exit from tail -f hit CTRL+C.

In the commands below that include “site.url“, be sure to switch this for your websites domain. For example:

```
cat /var/www/gridpane.com/logs/ssl-provision.log
```

### Server Logs

The gridpane.log logs what commands are run on your server.

```
/var/log/gridpane.log
```

### General Website Logs

The general logs keeps track of the changes made to your website in the site customizer. You can view changes that have been made to your site in this log. You can find them here:

```
/var/www/site.url/logs/gridpane-general.log
```

### Error Logs

You can view your websites Nginx error logs here:

```
/var/log/nginx/site.url.error.log
```

### Access Logs

The access.log logs the IP addresses of those that visit your websites, what they do, what browser they use, the names of the bots that crawl your site, and more.

```
/var/log/nginx/site.url.access.log
```

### SSL Renewal Logs

You can view your SSL renewal logs here. This includes renewals for all of your websites.

```
/opt/gridpane/certbot.monitoring.log
```

### SSL Provisioning Logs

To view the SSL provisioning logs for your individual websites you can find them in your websites /logs directory:

```
/var/www/site.url/logs/ssl-provision.log
```

### Single Sign On (SSO) Logs

View your websites single sign on logs:

```
/var/www/site.url/logs/sso.log
```

### Domains Log

The domains.log logs all of the changes made to your site, such as caching changes,

```
/var/www/site.url/logs/domains.log
```

### Debug Logs

If you’ve turned on WP Debug and need to see more of your debug log you can find it here (be sure to always turn debug off once you’ve finished using it):

```
/var/www/site.url/logs/debug.log
```

If you’d like to learn more about using WP Debug along with the Query Monitor plugin, check out this article.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

