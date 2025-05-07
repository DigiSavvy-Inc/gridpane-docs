# Configure Monit Service Management and Notifications with GP-CLI | GridPane

# Configure Monit Service Management and Notifications with GP-CLI

 

8 min read 

## Introduction

GridPane uses Monit to manage services and restart them if they start misbehaving. Sometimes you might wish to adjust these settings yourself – for example, if you think Monit is restarting MySQL too often.

You can completely customize the way Monit monitors and restarts the microservices on your servers, and when it sends notifications you alert notifications for each of them. This article will walk you through how this works, and how you can customize them with our GP-CLI.

MySQL and Redis are particularly useful for many use cases where you have larger than average websites.

Our defaults for the Nginx, OpenLiteSpeed, and PHP will very rarely ever need customizing, but you have the ability to do so should the need arise.

### Table of Contents

 

## gpmonit Syntax

gpmonit is our custom GP-CLI that’s specific to customizing Monit service monitoring and notifications on your GridPane servers.

Here is what the syntax looks like for customizing individual services:

 

```
gpmonit {service} \
-cpu-warning-percent {integer.percent} -cpu-warning-cycles {integer.cycles} \
-cpu-restart-percent {integer.percetn} -cpu-restart-cycles {integer.cycles} \
-mem-high-mb {integer.mb} -mem-high-cycles {integer.cycles} \
-mem-restart-mb {integer.mb} -mem-restart-cycles {integer.cycles} \
--debug \
--no-reload
```

You can run the command in the format shown above, or as a single line – whichever you prefer.

### For example:

```
gpmonit nginx \-cpu-warning-percent 50 -cpu-warning-cycles 5 \-cpu-restart-percent 70 -cpu-restart-cycles 5 \-mem-high-mb 800 -mem-high-cycles 10 \-mem-restart-mb 900 -mem-restart-cycles 10
```

Or:

```
gpmonit nginx -cpu-warning-percent 50 -cpu-warning-cycles 5 -cpu-restart-percent 70 -cpu-restart-cycles 5 -mem-high-mb 800 -mem-high-cycles 10 -mem-restart-mb 900 -mem-restart-cycles 10
```

### Output

This example results in the following settings for Nginx:

 

```
/etc/monit/conf.d/nginx:
-------------------------------------
# gridpane monit nginx v2
check process nginx with pidfile /var/run/nginx.pid
    group nginx
    start program = "/usr/local/bin/gp ngx start"
    stop program = "/usr/local/bin/gp ngx stop"
    if failed host 127.0.0.1 port 80 then restart
    if cpu > 50% for 5 cycles then exec "/usr/local/bin/gpmonitor NGINX CPU_HOT warning" AND repeat every 5 cycles
    if cpu > 70% for 5 cycles then exec "/usr/local/bin/gpmonitor NGINX CPU_RESTART error"
    if mem > 800 MB for 10 cycles then exec "/usr/local/bin/gpmonitor NGINX MEM_HIGH warning" AND repeat every 10 cycles
    if mem > 900 MB for 10 cycles then exec "/usr/local/bin/gpmonitor NGINX MEM_RESTART error"
    if 3 restarts within 5 cycles then exec "/usr/local/bin/gpmonitor NGINX FAILED error" AND repeat every 1 cycles
```

## Configuring Monit Service Monitoring Settings

Here we’ll take a look at the settings outlined in the example above for Nginx as an example.

I’ve replaced Nginx with “service“, as this all works the same way regardless of whether you’re configuring Nginx, OpenLiteSpeed, MySQL, Redis, and PHP.

 

 

### IMPORTANT CPU Info

When setting the CPU percentages in your settings you need to take into account the number of CPU cores your server has. For example, if you have 4 CPU cores, this means your CPU availability is 400%. 8 cores equals 800% and so on.

Setting your CPU to restart at 50% on a 4 core server, for example, would in practice restrict your CPU usage to 12.5% of the available resources and severely hamper your performance.

### 1. Service is using a lot of CPU Notifications

The two CPU hot commands let you customize when Monit sends you warning notifications for a specific service based on their sustained CPU usage:

```
-cpu-warning-percent 50 -cpu-warning-cycles 5
```

They set this line in their service-specific .env file:

```
if cpu > 50% for 5 cycles then exec "/usr/local/bin/gpmonitor SERVICE CPU_HOT warning" AND repeat every 5 cycles
```

This states that if the CPU consumption is over 50% for 5 cycles send a service is running hot warning message in the dashboard and slack (if applicable).

### 2. Service is using too much CPU Restarts

The two CPU restart commands let you customize when Monit will restart a service and notify you based on their sustained CPU usage:

```
-cpu-restart-percent 70 -cpu-restart-cycles 5
```

They set this line in their service-specific .env file:

```
if cpu > 70% for 5 cycles then exec "/usr/local/bin/gpmonitor SERVICE CPU_RESTART error"
```

This states that if the services CPU consumption is over 70% for 5 cycles then restart and send restart notification.

### 3. Service is using a lot of Memory Notifications

The two high memory usage commands let you customize when Monit sends you warning notifications for a specific service based on their high RAM usage:

```
-mem-high-mb 800 -mem-high-cycles 10
```

They set this line in their service-specific .env file:

```
if mem > 800 MB for 10 cycles then exec "/usr/local/bin/gpmonitor SERVICE MEM_HIGH warning" AND repeat every 10 cycles
```

This states that if the service consumes more than 800 MB of RAM for 10 cycles then send service High Memory warning.

### 4. Service is using too much Memory restarts

The two Memory restart commands let you customize when Monit will restart a service and notify you based on their high RAM usage:

```
-mem-restart-mb 900 -mem-restart-cycles 10
```

They set this line in their service-specific .env file:

```
if mem > 900 MB for 10 cycles then exec "/usr/local/bin/gpmonitor SERVICE MEM_RESTART error"
```

This states that if a service restarts 3 times within 5 cycles then send service failed warning notification every cycle until resolved. This message varies for different services.

 

### Monit Cycles

Monit runs in cycles, and one cycle = 2 minutes. So 5 cycles = every 10 minutes, 10 cycles = every 20 minutes etc.

 

### Customizing Individual Settings

You can customize individual settings by running the applicable commands, and leaving out those that you want to stay the same. For example, if you wanted to simply increase the CPU percent warning for MySQL, you could use this command:

```
gpmonit mysql -cpu-warning-percent 75
```

 

### View the Saved Settings

These commands rewrite their default templates and save the settings you pass to the following locations:

You can view each services current settings with the following command (replacing with the name of the service):
```
cat /etc/monit/conf.d/
```

For example:
```
cat /etc/monit/conf.d/mysql
```

 

### View all Current Settings

All configurations are stored in /root/gridenv/monit.env. You can view them with:

```
cat /root/gridenv/monit.env
```

 

## Debug and No-Reload Flags

Our CLI also includes two optional flags:--debug – shows more debug info.--no-reload – doesn’t reload Monit, so commands can be chained and reload on last one.

Simply add these to the end of the command you’re running. For example:

```
gpmonit mysql -cpu-warning-percent 55 --debug --no-reload
```

 

## MySQL

To configure Monit settings for MySQL the commands begin with: gpmonit mysql.

Here’s a placeholder command you can copy and adjust as per your requirements (switch out the integers with your settings):

```
gpmonit mysql \
-cpu-warning-percent 120 -cpu-warning-cycles 10 \
-cpu-restart-percent 180 -cpu-restart-cycles 5 \
-mem-high-mb 2692 -mem-high-cycles 10 \
-mem-restart-mb 3365 -mem-restart-cycles 10
```

### Common Use Case: Increase Memory Allocation

For sites that have a large database, allocating more memory to MySQL is often a good idea for performance, so that your entire database can be stored directly inside of RAM. A useful command for allocating more memory to MySQL is as follows:

```
gpmonit mysql \
-mem-high-mb 800 \
-mem-restart-mb 900
```

This command raises how much memory MySQL is allowed to consume before Monit restarts the service, and adjust the notifications accordingly as well.

Keep in mind that the more memory you allocate to one service, the less memory other services potentially have access to.

 

## Redis

To configure Monit settings for Redis the commands begin with: gpmonit redis.

Here’s a placeholder command you can copy and adjust as per your requirements (switch out the integers with your settings):

```
gpmonit redis \
-cpu-warning-percent 120 -cpu-warning-cycles 10 \
-cpu-restart-percent 160 -cpu-restart-cycles 5 \
-mem-high-mb 907 -mem-high-cycles 10 \
-mem-restart-mb 1207 -mem-restart-cycles 10
```

### Common Use Case 1: Increase Memory Allocation

A useful command for allocating more memory to Redis is as follows:

```
gpmonit redis \
-mem-high-mb 800 \
-mem-restart-mb 900
```

This command sets how much memory Redis is allowed to consume before Monit restarts the service, and adjusts the memory limit for warning notifications accordingly as well.

### Common Use Case 2: Reduce Warning Notifications

If you have websites on the server where they regularly consume a lot of memory via Redis, you may get repeated warning messages about high memory usage. You can reduce these by setting the -mem-high-mb setting to be higher than the -mem-restart-mb setting. With this, Redis will still notify you when Redis is restarted, but the advance warning messages will never fire as Redis restarts before they are triggered.

Run the following, replacing {integer} will a number a few hundred higher than the -mem-restart-mb:

```
gpmonit redis -mem-high-mb {integer}
```

 

## Nginx

To configure Monit settings for Nginx the commands begin with: gpmonit nginx.

Here’s a placeholder command you can copy and adjust as per your requirements (switch out the integers with your settings):

```
gpmonit nginx \
-cpu-warning-percent 100 -cpu-warning-cycles 5 \
-cpu-restart-percent 120 -cpu-restart-cycles 5 \
-mem-high-mb 1615 -mem-high-cycles 10 \
-mem-restart-mb 2826 -mem-restart-cycles 10
```

 

## OpenLiteSpeed

To configure Monit settings for OpenLiteSpeed the commands begin with: gpmonit openlitespeed.

Here’s a placeholder command you can copy and adjust as per your requirements (switch out the integers with your settings):

```
gpmonit openlitespeed \
-cpu-warning-percent 100 -cpu-warning-cycles 5 \-cpu-restart-percent 120 -cpu-restart-cycles 5 \-mem-high-mb 1615 -mem-high-cycles 10 \-mem-restart-mb 2826 -mem-restart-cycles 10
```

 

## PHP

Each version of PHP can be configured individually, so when running the commands before to use the correct version after gpmonit like so:

Here’s a placeholder command you can copy and adjust as per your requirements (switch out the integers with your settings and {x} for your PHP version):

```
gpmonit php7{x} \
-cpu-warning-percent 120 -cpu-warning-cycles 10 \-cpu-restart-percent 180 -cpu-restart-cycles 5 \-mem-high-mb 2692 -mem-high-cycles 10 \-mem-restart-mb 3365 -mem-restart-cycles 10
```

 

## Update Monit Settings

We also have CLI for updating Monit settings, which is particularly useful if you upgrade your server. The command is as follows:

```
gp server -update-monit
```

This will run all of these functions for each individual service. If a server has been resized it takes either the stored user .env value (the setting you have previously set with the GP-CLI detailed in this article) or the value based on our defaults for a server of that size.

It will use whichever is greater, and by using so this ensures that your server is able to make use of the new available resources, or doesn’t downgrade the settings you’ve already set.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

