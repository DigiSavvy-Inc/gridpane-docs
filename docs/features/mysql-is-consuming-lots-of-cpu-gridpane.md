# MySQL is Consuming Lots of CPU | GridPane

# MySQL is Consuming Lots of CPU

 

2 min read 

## Introduction

If MySQL is consuming a lot of your CPU resources or is maxing out your server, the best thing to do is log into MySQL on your server and watch the queries in real-time. This will clearly show what’s going on inside your database, and you will be able to diagnose what’s going on then and there or trace it back to a specific website on your server.

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Log into MySQL and Check Current Processes

Login to the server as root, and run:

```
gp mysql login root
```

Next, show processes with:

```
show processlist;
```

And you’ll see something like the following screen:

This screen will show which site is doing the query and what it’s doing.

### Table Locks

You may also see table-level locks, and if you do, you may want to consider switching to InnoDB, as it has row-level locking instead of table-level.

If you see “Waiting for table metadata lock”, you’re experiencing table locking. Here’s an example of what this looks like:

 

```
mysql> show processlist;
+-------+---------------------+-----------+---------------------+---------+--------+---------------------------------+------------------------------------------------------------------------------------------------------+-----------+---------------+
| Id    | User                | Host      | db                  | Command | Time   | State                           | Info                                                                                                 | Rows_sent | Rows_examined |
+-------+---------------------+-----------+---------------------+---------+--------+---------------------------------+------------------------------------------------------------------------------------------------------+-----------+---------------+
|     5 | event_scheduler     | localhost | NULL                | Daemon  | 558150 | Waiting on empty queue          | NULL                                                                                                 |         0 |             0 |
| 34478 | VOO_example_com | localhost | VOO_example_com | Sleep   |  70388 |                                 | NULL                                                                                                 |         0 |             0 |
| 34479 | VOO_example_com | localhost | NULL                | Sleep   |  70388 |                                 | NULL                                                                                                 |      6230 |          6230 |
| 34480 | VOO_example_com | localhost | NULL                | Sleep   |  70387 |                                 | NULL                                                                                                 |    748034 |        748034 |
| 40581 | VOO_example_com | localhost | VOO_example_com | Query   |  14241 | Waiting for table metadata lock | DROP TABLE IF EXISTS wp_bv_ip_store                                                                  |         0 |             0 |
| 40582 | VOO_example_com | localhost | VOO_example_com | Query   |  14140 | Waiting for table metadata lock | DROP TABLE IF EXISTS wp_bv_ip_store                                                                  |         0 |             0 |
| 40583 | VOO_example_com | localhost | VOO_example_com | Query   |  14040 | Waiting for table metadata lock | DROP TABLE IF EXISTS wp_bv_ip_store                                                                  |         0 |             0 |
| 40984 | VOO_example_com | localhost | VOO_example_com | Query   |  12582 | Waiting for table metadata lock | SELECT * FROM wp_bv_ip_store WHERE '�<:' >= `start_ip_range` && '�<:' <= `end_ip_range` && `is_lp`   |         0 |             0 |
| 40985 | VOO_example_com | localhost | VOO_example_com | Query   |  12518 | Waiting for table metadata lock | SELECT * FROM wp_bv_ip_store WHERE '�<:' >= `start_ip_range` && '�<:' <= `end_ip_range` && `is_lp`   |         0 |             0 |
```

### Sleeping Queries

Sleeping queries are mostly inactive open connections. When there’s a build up it can bring your website to a halt. This would in turn cause the server to be unable to process more queries.

Clearing sleeping queries is a little different to clearing table locks. In this case, you can stop and then start MySQL. Stop it with:

```
gp mysql -stop
```

Wait for approximately 5 seconds and then start MySQL again with:

```
gp mysql -start
```

 

## One or More of Your Websites are Too Busy

A busy website can mean that it’s simply receiving a great deal of live traffic, or it’s under some kind of attack. These can overwhelm a server if there’s not a

The effect is largely the same if it’s maxing out the resources, but you should be able to quickly tell if it’s an attack or not by checking your access logs and seeing what’s being hit on your site. If it’s the same IP/s over and over again hitting the same pages, then it’s likely an attack.

Misconfigured PHP workers can also dramatically worsen the problem by creating a huge backlog of PHP requests that the server can never handle.

This requires standard website debug. You should first check if your site is in fact under attack – start at section 2 in this article:

Mitigating DoS and DDoS Attacks On Your WordPress Websites

If you’re experiencing 504 errors or a mix of 504 and 502 errors, you should follow this article, which is essentially the step-by-step guide for dealing with any kind of performance-related issues:

Diagnosing 504 Timeouts and Performance Issues

 

## MySQL Slow Logging

MySQL slow query logging can be a highly useful tool for uncovering performance bottlenecks in your websites.

The MySQL slow query log is where the MySQL database server will log all queries that exceed a time (in seconds) that you specify. This can be particularly helpful on database-intensive websites, such as WooCommerce stores, to help identify long-running processes, so that you can set about fixing them for better performance. Learn more here:

Using the MySQL Slow Log

 

## MySQL: Convert MyISAM Tables to InnoBD

A lot of the time, when we see a performance-related issue on a website, it’s related to the database not being optimized.

 

 

### Information

This section should be followed only after the first two sections above.

MyISAM is often a primary culprit and is an older, less efficient, and less reliable database storage engine than the more modern InnoDB.

Part of the reason for this is that MyISAM will lock whole database tables, which can have a logjam effect on database queries, whereas InnoDB only has row-level locking, which allows queries to process much faster. Converting can result in huge improvements in response time and reduced server load.

By default, GridPane uses InnoDB, but older websites sometimes use MyISAM, and sometimes websites will have a mix of both. This article will walk you through how to convert MyISAM to InnoDB:

Converting MyISAM to InnoDB

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

