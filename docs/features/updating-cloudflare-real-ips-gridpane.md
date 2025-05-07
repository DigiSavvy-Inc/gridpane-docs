# Updating Cloudflare Real IPs | GridPane

# Updating Cloudflare Real IPs

 

4 min read 

 

### Written By Thomas Raef

This article was contributed by Thomas Raef, the founder of  WeWatchYourWebsite.com. Thomas runs a website protection, monitoring and malware removal service and is one of a very, very short list of people who we recommend for this service.

## Introduction

In the course of analyzing log files for both SEO and security concerns, one of the most defeating occurrences is wrong IP addresses in the logs.

Many of you are using Cloudflare on your sites. Some of you use it for the CDN, some for added security. Whatever your reason, you must do the steps detailed below.

Your log files show the IP address of the last leg of the transaction between your website and the source. If you have Cloudflare configured for your website, it becomes the source. It’s the last leg of the transaction.

When we analyze logs for malicious activity, one of the items of key importance is the IP address. For instance, if we see someone from Ukraine logging into your WordPress dashboard, it becomes highly suspicious – unless you have developers in Ukraine.

If your Cloudflare isn’t configured correctly, or more accurately if your Nginx isn’t configured properly, we won’t know that this was sourced in Ukraine because the log file will only show the last IP address of the Cloudflare server your traffic was delivered from.

 

## Configuring Daily Real IP Updates

GridPane provides a common configuration and they do update real IPs regularly, but you can set the following up to update these every day.

### Step 1. Create the Daily Update Shell Script

This shell script will contact the Cloudflare servers once a day and create a new updated list of their server blocks. Then the shell will restart Nginx upon successful completion of the update.

You can cut and paste this script into a file named: cloudflare-updates.sh and place it in the /opt/gridpane folder.

*The script below as updated by the GridPane team on August 30th 2022.

 

```
#!/bin/bash

CLOUDFLARE_PATH=/etc/nginx/common/cloudflare-realip.conf

# let’s make a backup of the cloudflare-realip.conf file, if it exists.

if test -f $CLOUDFLARE_PATH; then

cp /etc/nginx/common/cloudflare-realip.conf{,.bak}

fi

echo "# #" > $CLOUDFLARE_PATH;

echo "# Cloudflare" >> $CLOUDFLARE_PATH;

echo "# Real IPs" >> $CLOUDFLARE_PATH;

echo "# IPv4 list https://www.cloudflare.com/ips-v4" >> $CLOUDFLARE_PATH;

echo "# IPv6 list https://www.cloudflare.com/ips-v6" >> $CLOUDFLARE_PATH;

echo "# #" >> $CLOUDFLARE_PATH;

for i in `curl https://www.cloudflare.com/ips-v4`; do

echo "set_real_ip_from $i;" >> $CLOUDFLARE_PATH;

done

for i in `curl https://www.cloudflare.com/ips-v6`; do

echo "set_real_ip_from $i;" >> $CLOUDFLARE_PATH;

done

echo "" >> $CLOUDFLARE_PATH;

#echo "real_ip_header CF-Connecting-IP;" >> $CLOUDFLARE_PATH;

#test configuration and then reload nginx

if nginx -t; then

systemctl reload nginx

else

echo "Something went wrong with the nginx -t. I suggest you type it from the command prompt."

echo "We are going to revert to the last working copy until this is resolved."

cp /etc/nginx/common/cloudflare-realip.conf.bak /etc/nginx/common/cloudflare-realip.conf

systemctl reload nginx

exit 1

fi

## end of file
```

Save that file with CTRL+O followed by Enter, then exit nano with CTRL+X.

Then from the command line enter:

```
chmod +x /opt/gridpane/cloudflare-updates.sh
```

#### GridPane Includes

GridPane automatically loads the cloudflare-realip.conf into Nginx. Each individual websites vhost contains this include:

```
include /etc/nginx/common/gridpane-realip.conf;
```

And this include contains:

```
include /etc/nginx/common/*cloudflare-realip.conf;
```

 

### Step 2. Create a Cronjob to Run the Shell Script

We need to set our new script to update every day, as Cloudflare publishes new IP addresses every day.

Edit your crontab with:

```
crontab -e
```

Paste the following two lines at the bottom of the file:

```
#This script updates the list of Cloudflare servers every day at midnight, server time.
0 0 * * * /opt/gridpane/cloudflare-updates.sh
```

Save the file with CTRL+O followed by Enter, and exit nano with CTRL+X.

You’ll now always see the original IP addresses in your log files instead of all your traffic looking like it originated at Cloudflare.

If you ever do need forensic analysis or SEO analysis, you’ll be working with correct data.

 

 

### If you enjoyed this article...

Thomas has contributed multiple articles to the GridPane knowledge base, all of which are listed below:

The OWASP Top 10 and GridPane WordPress Security Options
Server Provider Attack Warnings: How to Find Brute Force Malware
Updating Cloudflare Real IPs

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

