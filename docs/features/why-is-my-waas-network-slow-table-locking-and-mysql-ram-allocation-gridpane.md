# Why is my WaaS network slow? Table locking and MySQL RAM allocation | GridPane

# Why is my WaaS network slow? Table locking and MySQL RAM allocation

 

4 min read 

WaaS networks are database intensive websites, and this is something many WaaS networks go through as they begin to grow in size and traffic.

Sometimes this is because the server simply isn’t big enough for the network anymore, and sometimes it can be solved by increasing the MySQL’s RAM allocation.

This article will walk you through how to confirm is database table locking is the source of your problem, and then the steps you can take to resolve the issue.

## Part 1. Confirm the Problem

First, we need to ensure that the problem is indeed table locking.

### SSH into your server

To check, you’ll need to SSH into your server. Please see the following articles to get started:

Generate your SSH Key:

Generate SSH Key on Mac

Generate SSH Key on Windows with Putty

Generate SSH Key on Windows with Windows Subsystem for Linux

Generate SSH Key on Windows with Windows CMD/PowerShell

Add your SSH Key to GridPane:

Add default SSH Keys

Add/Remove an SSH Key to/from an Active GridPane Server

Connect to your server:

Connect to a GridPane server by SSH as Root user.

### Diagnosis

To check if you have locked database tables, run the following command:

```
gp mysql login root
```

You are now logged into MySQL. Check your active processes with:

```
show processlist;
```

If you see “Waiting for table metadata lock”, you’re experiencing table locking.

You can exit MySQL with:

```
exit
```

## Part 2. How to Fix it

If you need to get this sorted immediately, you can kill these queries by restarting MySQL. You can do this on your server with:

```
service mysql restart
```

And you can also restart MySQL to kill these queries inside of Monit.

Also, for reference, you can stop and start MySQL with:

```
service mysql stop
service mysql start
```

## Part 3. Reasons For Table Locking & Improving Performance Moving Forward

### Hourly Backups

If you’re experiencing these issues around the start of every hour, this is likely related to your backup system, Borg, running and locking your tables while it takes the backups. If you have a large website that takes a long time to backup, this could frequently impact your performance for extended periods of time.

You may wish to adjust your backup schedule. You can also learn how to do this here:GridPane Local and Remote Backups

### Database Optimization

If it’s not simply a backup related issue, then you can try optimizing your database, and converting any MyISAM tables to InnoDB for better performance.

You can learn how to convert your database tables here:

Converting MyISAM to InnoDB

You can learn how to optimize your database tables here:

How to Optimize Databases to Reduce Bloat

You may also want to check out the following two database optimization plugins – both of which are great in our experience. Just be sure to take a backup before making changes to any of your databases.

### Increase RAM Allocation

You can also try allocating additional RAM to MySQL – for large WaaS networks, it’s usually a good idea to be able to have your entire database stored in RAM. The better optimized your database, the less RAM you’ll need for this.

Please keep in mind that the more memory you allocate to MySQL, the less will be available for your servers other processes, and this may create a whole new load of problems. We don’t recommend allocating more than 50% of your RAM to MySQL.

To begin, run the following command

```
nano /etc/monit/conf.d/mysql
```

A typical file looks like this:

```
Check process mysql with pidfile /var/run/mysqld/mysqld.pid
    group database
    group mysql
    start program = "/usr/sbin/service mysql start"
    stop program = "/usr/sbin/service mysql stop"
    if cpu > 60% for 2 cycles then alert
    if cpu > 70% for 3 cycles then exec "/usr/local/bin/gpslack MYSQL_HOT warning"
    if cpu > 90% for 5 cycles then restart
    if mem > 550 MB for 3 cycles then restart
    if failed host localhost port 3306 protocol mysql with timeout 15 seconds for 3 times within 4 cycles then restart
    if failed unixsocket /var/run/mysqld/mysqld.sock protocol mysql for 3 times within 4 cycles then restart
    if 3 restarts within 5 cycles then exec "/usr/local/bin/gpslack MYSQL error"
```

To adjust MySQL’s memory limit adjust this line, for example:

```
if mem > 750 MB for 3 cycles then restart
```

We recommend small increases up to the 50% of total memory mark, and if you’re still experiencing issues after that, you need to look at your database performance or increase your server size.

Once you’ve adjust the above line, hit Control+O, then enter to save the file. Then Control+X to exit nano.

Next you need to reload Monit:

```
monit reload
```

Test and repeat, then continue below if necessary.

## Further Reading

We have several articles on troubleshooting database performance that you may find valuable. Below are links to each of them.

Where to start with determining where a performance issue exists?

MySQL is taking up a LOT of disk space. Why?

MySQL is consuming lots of CPU

Diagnosing and Fixing: “Error Establishing a Database Connection”

How to backup / export / import a WordPress database

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

