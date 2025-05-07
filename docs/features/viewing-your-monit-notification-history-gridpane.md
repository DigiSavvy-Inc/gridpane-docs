# Viewing Your Monit Notification History | GridPane

# Viewing Your Monit Notification History

 

3 min read 

### Table of Contents

 

## Introduction

GridPane uses Monit to manage services and restart them based on criteria such as extended periods of high CPU or RAM usage over a set period of time.

Monit will send notifications within your GridPane account and to Slack (if set up). These notifications are logged on your server and time-stamped. Should you encounter any issues, they may be helpful in troubleshooting issues such as 502/504 timeouts and more.

In this article, we’ll dig into the available GP-CLI.

### Connect to your server

You’ll need to connect to your server to run the CLI commands. If this is your first time connecting to one or your servers, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Viewing All Notification History

To view your Monit notification history for all entries from our gpmonit triggers of gpmonitor, you can run the following command:

```
gpmonit -history
```

The output will look as follows, with the most recent notifications at the bottom:

```
May 19 20:59:48 aws-nginx-mariadb root[831]: ***** GridPane Monitoring - FILESYSTEM Capacity Warning > 80% ***** The Filesystem on aws-nginx-mariadb 35.159.0.17 has surpassed 80% disk capacity. Please consider upgrading your disk space.May 19 21:00:22 aws-nginx-mariadb root[4185]: ***** GridPane Monitoring - FILESYSTEM Capacity Warning > 85% ***** The Filesystem on aws-nginx-mariadb 35.159.0.17 has surpassed 85% disk capacity. Really, it would be a great idea to scale your disk up now...May 19 21:00:32 aws-nginx-mariadb root[4362]: ***** GridPane Monitoring - FILESYSTEM Capacity Warning > 90% ***** The Filesystem on aws-nginx-mariadb 35.159.0.17 has surpassed 90% disk capacity. Please consider upgrading your disk space.May 20 20:52:24 aws-nginx-mariadb root[18063]: ***** GridPane Monitoring - FILESYSTEM Capacity Warning > 95% ***** The Filesystem on aws-nginx-mariadb 35.159.0.17 has surpassed 95% disk capacity. Really, it would be a great idea to scale your disk up now...May 20 20:52:25 aws-nginx-mariadb root[18108]: ***** GridPane Monitoring - FILESYSTEM Capacity Warning > 98% ***** The Filesystem on aws-nginx-mariadb 35.159.0.17 has surpassed 98% disk capacity. This is bad, things are about to go south... please scale up before it is too late...May 20 20:52:27 aws-nginx-mariadb root[18153]: ***** GridPane Monitoring - FILESYSTEM Capacity Warning > 99% ***** The Filesystem on aws-nginx-mariadb 35.159.0.17 has surpassed 99% disk capacity. Okay, this is where things are going to cascade fail... so long and thanks for all the fish!!!May 20 20:52:28 aws-nginx-mariadb root[18204]: ***** GridPane Monitoring - MYSQL CPU_HOT Warning ***** MYSQL on aws-nginx-mariadb 35.159.0.17 has been using 70% of CPU for over 20 minutes...May 20 20:52:32 aws-nginx-mariadb root[18513]: ***** GridPane Monitoring - MYSQL CPU_RESTART Error ***** MYSQL on aws-nginx-mariadb 35.159.0.17 was using 90% of CPU for over 30 minutes... restarting MYSQL!May 20 20:52:33 aws-nginx-mariadb root[18579]: ***** GridPane Monitoring - MYSQL MEM_HIGH Warning ***** MYSQL on aws-nginx-mariadb 35.159.0.17 has been using at least 711MB RAM for at least the last 20 minutes...May 20 20:52:36 aws-nginx-mariadb root[18947]: ***** GridPane Monitoring - MYSQL MEM_RESTART Error ***** MYSQL on aws-nginx-mariadb 35.159.0.17 has been using at least 800MB RAM for at least the last 40 minutes.... restarting MYSQL!
```

All Monit warnings and events are now stored in the /var/log/syslog. This GP-CLI command will check the log and format it into the above output.

 

## Viewing Individual Service Notifications

You can also specify a specific service and use the following to view only notifications for that service:

```
gpmonit -history {monitor}
```

Each of the individual 16 monitors in the box below can be viewed, and as noted at the end of the very last line, you can view ALL PHP notifications or only those specific to an individual version.

```
fail2ban
filesystem
mysql
nginx
redis
openlitespeed
sys_load_avg|sys_mem_usage|sys_cpu_usage|sys_swap_mem|system
php7.1|php7.2|php7.3|php7.4|php
```

### Example Commands

For example to view MySQL history, run:

```
gpmonit -history mysql
```

For the System Load Average notifications run:

```
gpmonit -history sys_load_avg
```

Simply add your desired monitor to end of gpmonit -history and hit enter.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

