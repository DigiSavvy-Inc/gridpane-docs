# Adjusting MySQL Monit Memory | GridPane

# Adjusting MySQL Monit Memory

 

2 min read 

## Introduction

GridPane uses Monit to manage services and restart them if necessary to ensure the stability of your server. We set MySQL to restart if it starts using too much CPU or Memory, and we set thresholds based on the amount of RAM and number of CPUs.

Sometimes you might wish to adjust these settings yourself if you think Monit is restarting MySQL too often, or if you have a lot of RAM. This is most likely to be the case if you need to adjust its memory headroom.

You’ll need to connect to your server to run the commands. Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## View Your Monit MySQL Config

The typical Monit MySQL configuration for a 2 GB RAM server it can be found here:

```
cat /etc/monit/conf.d/mysql
```

 

```
# gridpane monit mysql v2
check process mysql with pidfile /var/run/mysqld/mysqld.pid
    group database
    group mysql
    start program = "/usr/sbin/service mysql start"
    stop  program = "/usr/sbin/service mysql stop"
    if cpu > 70% for 10 cycles then exec "/usr/local/bin/gpmonitor MYSQL CPU_HOT warning" AND repeat every 10 cycles
    if cpu > 90% for 15 cycles then exec "/usr/local/bin/gpmonitor MYSQL CPU_RESTART error"
    if mem > 711 MB for 10 cycles then exec "/usr/local/bin/gpmonitor MYSQL MEM_HIGH warning" AND repeat every 10 cycles
    if mem > 711 MB for 20 cycles then exec "/usr/local/bin/gpmonitor MYSQL MEM_RESTART error"
    if failed host localhost port 3306 protocol mysql with timeout 15 seconds for 3 times within 4 cycles then restart
    if failed unixsocket /var/run/mysqld/mysqld.sock protocol mysql for 3 times within 4 cycles then restart
    if 3 restarts within 5 cycles then exec "/usr/local/bin/gpmonitor MYSQL FAILED error" AND repeat every 1 cycles
```

As you can see, Monit allows MySQL to run with 30% of the available RAM. We consider this about right for such a small server, but you might still want to adjust this.

 

## GP-CLI for Adjusting Monit MySQL Thresholds

There is now GP-CLI available to help you easily configure these settings on the command line. You can learn more about how it all works in this article:

Configure Monit Service Management and Notifications with GP-CLI

To configure Monit settings for MySQL the commands begin with: gpmonit mysql.

### Increase Memory Allocation

For this example, we could use the following settings to allow MySQL to run with 50% of the RAM:

```
gpmonit mysql \
-mem-high-mb 900 \
-mem-restart-mb 1024
```

This command raises how much memory MySQL is allowed to consume before Monit restarts the service, and adjust the notifications accordingly as well.

Keep in mind that the more memory you allocate to one service, the less memory other services potentially have access to.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

