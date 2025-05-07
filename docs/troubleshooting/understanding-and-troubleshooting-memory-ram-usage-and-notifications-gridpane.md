# Understanding and Troubleshooting Memory (RAM) Usage and Notifications | GridPane

# Understanding and Troubleshooting Memory (RAM) Usage and Notifications

 

8 min read 

### Table of Contents

 

## Introduction

RAM usage is a topic we receive a lot of questions about, especially if a server is using more RAM than you might expect.

RAM usage, in general, is a good thing. Both Linux and the services that power your websites (PHP, MySQL, Redis, Nginx, and OpenLiteSpeed) perform far better when in RAM, rather than loading up when needed.

In fact, if you’ve recently migrated from our 18.04 stack to our 22.04 stack, you may notice a performance improvement across your sites due to new RAM allocation settings, which allow for more MySQL memory usage out of the box (more info below).

This article will explain why and where your RAM is being used and the most common causes of high memory usage.

 

## Monit and Notifications

Monit monitors individual services as well as the overall system load. For memory, you may see the following warning notifications when your services or system average reaches the set threshold:

It’s also possible to see this for Nginx and OpenLiteSpeed, but extremely unlikely.

### Services vs System

The PHP, MySQL, and Redis warning notifications are sent when these individual services are close to their set memory allowances, but these can be adjusted on servers with clearly enough free memory.

The SYS_MEM_USAGE warning is when the overall memory usage on the server is hitting different thresholds (you’ll see a percentage in the notification).

### Configuring Notifications

If you’re regularly seeing notifications for high memory usage but see there is plenty of available RAM on the server, you can tweak these notifications. This is measured on a percentage basis, and servers that have many GB of memory free due to their large size may throw warnings even when there is plenty of free space. Please see the following article for step-by-step instructions on how to adjust these settings:

Manually Configure Monit/Slack Notifications for Disk Space Warnings

 

## Understanding Memory (RAM) Usage

The following outlines where RAM is used on your servers so that you have an understanding of where to look if you need to troubleshoot high memory warnings.

 

### Ubuntu OS

The Ubuntu operating system, like any OS, requires RAM to run smoothly. Fortunately, Ubuntu uses very little RAM. However, on Ubuntu 22.04, you may see higher RAM usage than on previous stacks. Learn more here ▼

 

### MySQL

MySQL memory usage depends on three different factors:

MySQL Version: On GridPane, different versions of Ubuntu run different versions of Percona and MariaDB. The newer version of MariaDB uses more RAM than previous versions.

Collective Database Size: For your WordPress websites, loading your databases into RAM will happen naturally, though the process isn’t instant (which is why a MySQL restart can sometimes alleviate high memory issues temporarily). The upside is that this offers a significant performance benefit, especially for dynamic websites such as WooCommerce.

Server Allowance: Different server sizes have different memory allowances to maintain the stability of your system – lower memory servers have a lower allowance to take into the baseline memory needed for the Ubuntu OS, PHP, MySQL, and Nginx to operate.

 

### Redis

Redis is a high-performance in-memory database. For WordPress purposes, it is primarily used as a key-value store for object caching and page caching on our Nginx stack. Redis can dramatically increase your website’s speed, reducing the burden of work off of MySQL and/or PHP.

Our default values are fine for most websites, but you may see memory-related warnings on smaller 2GB RAM servers.

Warnings on larger servers likely mean that one or more websites have a very large database.

 

### PHP

Different versions of PHP will each use around 280MB of RAM each by default. On top of that, the main two sources of RAM are PHP workers and the collective page cache size of your websites.

Please note that too many active PHP workers are one of the most common reasons we see higher than healthy RAM usage on a server.

 

### Nginx / OpenLiteSpeed

Nginx and OpenLiteSpeed will typically each use a few hundred MB. Nginx requires a little more on Ubuntu 22.04 than on previous versions of Ubuntu.

It is extremely rare for either Nginx or OpenLiteSpeed to use a significantly high amount of RAM.

 

## Ubuntu 22.04 and Memory Usage

With the 22.04 stack, there are some additional factors that may result in an increase of memory (RAM) usage on your servers compared to 18.04 and 20.04.

### MySQL Allowances

We’ve increased the amount of baseline RAM available to MySQL via the InnoDB buffer pool so that as MySQL operates, it loads as much of its data directly into RAM as possible. Previously, the baseline for all servers was considerably lower and we offered the ability for you to increase it as needed. However, this was rarely implemented, and based on the data we’ve gathered since 2018, we have set the baseline to a higher amount on this latest stack.

We now allow 25-33% of RAM on newer 22.04 servers depending on the available RAM, and so now for a 4 GB RAM server this is an allowance of 1338 MB instead of 128MB on previous stacks.

This additional memory increase allows much faster processing and enables MySQL to keep more data in buffer instead of just writing it on to disk at once.

### Service Memory Usage

MySQL: In addition, the 22.04 versions of MySQL use more RAM than before (MariaDB 10.11 comes with more features than the previous 10.3), but these memory increases offer increased performance.

PHP: The same is again true of PHP running on 22.04, and there are noticeable performance improvements.

Nginx: This version of Nginx also uses a little more RAM, but this is marginal (in the couple of hundreds of MB).

 

## The Primary Reasons for High Memory (RAM) Usage

There are three primary reasons we see behind high memory usage on a server:

Another potential reason is that your website/s cache is enormous, which can happen when sites have a high number of pages. This will be seen in high memory usage in either PHP or Redis, but is far more rare.

### Monit has Answers

To see where RAM is being used on a given server, head over to the Sites page inside your account:

And then click on the server pie chart icon for the server you’re inspecting:

This will open up the Monit status page for your server. Here, you can view the amount of memory in use for your services and overall system usage:

If you see that MySQL is consuming a lot of RAM, you can check the size of MySQL (which includes the collective size of your databases) in the section directly below:

 

## Reducing Memory Usage

Sometimes, the right call for your server is to increase it’s size as the site or sites in question require more memory to function correctly.

However, it may be that you’ve misconfigured your PHP workers, or a database on one or more of your sites has grown out of control. In these cases, you can free up memory space and avoid the need to scale your server up in size.

### Reduce PHP Workers

If the cause of your high memory is PHP, you can reduce the number of PHP workers where there are clearly too many for the server – this could include switching them from Static to Dynamic on production sites, and/or changing them to Ondemand on staging, and reducing the overall number of PHP workers (PM Max Children) across your websites.

These can be changed inside the website customizer in the PHP tab:

We typically recommend 3-4 workers per 1 CPU core, and usually recommend Dynamic workers for most websites.

Learn more about PHP workers and further settings recommendations here:

PHP Workers and WordPress: A Guide for Better Performance

### Optimize Your Databases

You may be able to significantly reduce the size of one or more of your website databases, which can significantly decrease memory usage.

Database bloat can come from many different places. For example, thousands of page revisions from working with pagebuilders, poorly coded plugins gone out of control, or InnoDB has bloated up, and there is space that can be reclaimed.

Please see this article for more details on how to reduce database bloat (and always be sure to take a backup before working on your databases):

How to Optimize Databases to Reduce Bloat

### Clear the Cache and Reduce Cache TTL

This is a temporary solution, but it can potentially clear out RAM, providing some relief to your server in the short term. Reducing the cache TTL on OpenLiteSpeed or Nginx Redis Object caching may also help keep the size of the cache lower on average (and note that this won’t help on Nginx FastCGI as it uses microcaching).

### Move “Problem” Websites to Their Own Server

If you have one site in particular that is causing issues on a server, you may be better off simply moving this site to it’s own server, or a server that has resources to spare.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

