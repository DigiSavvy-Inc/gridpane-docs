# Diagnosing 504 Timeouts and Performance Issues | GridPane

# Diagnosing 504 Timeouts and Performance Issues

 

10 min read 

### Table of Contents

If you’re experiencing issues only when trying to log into your website and/or inside the /wp-admin area, your website has a codebase issue. Skip to the last section.

 

 

### IMPORTANT

Unlike a 502 error where PHP or Nginx may be down, 504 errors almost never indicate an issue with the server stack.

## DIAGNOSIS STEPS BREAKDOWN

###### Check Monit:

###### Check top and htop:

###### Check MySQL:

### At this point you should have an idea of what’s going on and what’s responsible, including which site/s if applicable.

###### Website Database:

###### Website PHP Settings:

###### Error and WP Debug logs:

###### Access Logs:

 

## Introduction

504 Gateway Timeout errors are one of the most common performance-related errors.

In a nutshell, they occur when a server “didn’t receive a response from an upstream server it needed to access in order to complete the request“.Source:  Internet Engineering Task Force

The messaging that displays with your 504 error may vary, but the variations don’t indicate any specific issues. Here are a few common examples:

### 504 Debug

This article details a step-by-step checklist to diagnose your 504 errors by quickly narrowing down the root of the cause.

 

## What Causes a 504 Error?

Here are four categories of issues that can cause 504s:

###### 1. Database/codebase issues

###### 2. Server overload

###### 3. Not enough resources on your server

###### 4. Proxy/CDN issue

It’s not your server or your website, but a service between you and the server that’s having issues.

### Real World Examples

### But my Codebase hasn’t changed?

Even if this is true, that doesn’t mean that errors can’t still happen. High traffic can quickly reveal inefficiencies in your codebase, as well as run into major performance bottlenecks of your sites PHP settings have been misconfigured or require excessive amounts of PHP Memory.

 

 

### Plugins and 504 Errors

Plugins we've seen to be directly responsible for 504 errors in some cases include Blogvault, MalCare, and Rankmath Pro.  We've also seen a conflict with Learndash and Oxygen cause 504s. We will update this article with more information as it becomes available. The cause of these errors is often fixed in future updates.

## 1. Check Monit

First, head to your Servers page in your account and open up Monit for the server you’re having trouble with by clicking on the pie chart icon:

Does the server look healthy? Here we’re looking for anything highlighted in red, and specifically at the CPU and RAM usage at the very top. Here’s a healthy example:

This will tell you a lot about what’s going on inside your server.

Here you need to determine whether or not you have the resources available for your server to run efficiently. If your server is all green and your CPU and RAM seem fine, then it’s likely going to be one of the following:

### FILESYSTEM: Space usage is above 90%

A common thing we see is disk space being over 90% full and starving the server’s processes of memory, which in turn causes temporary 504 errors.

Space usage is the amount of available disk space on your server. If it’s in the red, you may need to clean up some space or resize your server to the next size up.

This is likely the cause of your problem.

### SYSTEM: High CPU usage

Sustained high CPU usage means that your server is experiencing a heavy amount of processes, which could mean: –

If you’re experiencing high CPU and RAM usage, proceed to step 4.

### PROCESSES: Nginx, MySQL or PHP are busy

If one of your services is busy – e.g. your PHP version, Nginx, or MySQL, then this may be the root cause of your timeouts – the server is there, but visitors can’t retrieve any information because your services are locked up in other long running tasks.

These need to be fixed – either by restarting them, or allocating more memory to them so they can do what they need to do.

This is likely the cause of your problem.

### System: High Memory Usage

If there’s not enough free memory and/or your system is utilizing a lot of swap, this can slow loading your websites down to a crawl.

PHP worker misconfiguration is often a cause of this, but very large databases (or collectively large databases), misconfigured PHP INI settings, massive sites with huge FastCGI caches, sites that need A LOT of memory to function that are getting a lot of traffic.

 

## 2. Check top and htop

Here we want to check two things:

The goal is to identify what service and/or websites are most active so that you know the next step to take in your troubleshooting.

For this you’ll need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Checking for CPU steal and IOwait with TOP

The top command will let you know if other VPS’s on your server are stealing your CPU usage, or if your CPU is waiting on IO/drives. Run:

```
top
```

And you’ll see a table appear that looks as follows. We’re interested in the parts highlighted in red:

#### Steal “st”

Here you can see there’s no steal, but sometimes neighbours on your server can potentially steal a lot of your CPU – sometimes over 50% or more.

If you’re experiencing server steal then you need to contact you IaaS provider directly to let them know what’s going on so they can take action accordingly.

#### I/O Wait “wa”

If this is high then the CPU is waiting on the IO/drives. You can exit top and install run iotop to see which process is causing the most I/O utilization on your server.

To exit top hit Ctrl+C.

You can install iotop with:

```
apt install iotop
```

Then run:

```
iotop
```

iotop will list all of the processes running with the heaviest process at the very top.

If your steal and wait time are clear, then proceed below. To exit top/iotop hit Ctrl+C.

### Checking active processes with HTOP

The information presented by htop will identify the processes responsible for high resource usage on the server. By default, processes are sorted by CPU usage – the highest at user at the very top of the table. To get started run:

```
htop
```

This will open up a table that looks like the following:

Here you’ll be able to see what’s going on and which of your websites are responsible for any high usage.

If you identify your site, you now dig deeper into what’s going on at the website level. It may also be that a different site than you were expecting is the root of the cause. To exit htop hit Ctrl+C.

You can learn more about using top and htop in these articles:

 

## 3. Check MySQL

### Database Table Locking / Sleeping Queries

Table lock is one of the most common causes behind both 502 and 504 errors. You can check to see if you have any locked tables by first running:

```
gp mysql login root
```

And then run:

```
show processlist;
```

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

This particular example was MalCare, which shares the same table prefix with Blogvault – another plugin we’ve seen at the cause. Other plugins we’ve seen include Cleantalk, Rank Math, and WPvivid.

Exit MySQL with:

```
exit
```

###### How to Fix it

You can restart MySQL with the following command:

```
gp mysql restart
```

You can also restart MySQL inside of Monit as well.

We sometimes see this on WaaS networks. Multisites are heavy on database processes and you may be experiencing table locking. You’ll want to ensure that your using InnoDB and not MyISAM as above, and then determine whether this is related to our backup system.

###### Local Website Backups

If you’re experiencing these issues around the start of every hour, this is maybe related to our older backup system, Borg, running and locking your tables while it takes the backups. If you have a large website that takes a long time to backup, this could frequently impact your performance for extended periods of time.

 

## 4. Check Your Website Database

### Impaired Database

A corrupt WordPress database may also trigger a 504 gateway timeout error. You check the status of your database using GP-WP-CLI. Inside your server run the following replacing “site.url” with your domain name:

```
gp wp site.url db check
```

If you find any crashed tables you can repair them with the following command – but always make sure you have a backup before doing any kind of database work:

```
gp wp site.url db repair
```

### Is your database slow, impaired, or lacking resources?

Is your website’s database slowing things down? Following the Query Monitor guide above should help you in determining this, but here are some things we see on support.

###### MyISAM

If your database is using MyISAM instead of InnoDB, this may be seriously harming your website’s performance. Check out our guide on converting MyISAM to InnoDB here:

Converting MyISAM to InnoDB

 

## 5. Check Your Website Debug/Error Logs

### Is a plugin erroring and causing your website to run slow?

The best way to begin diagnosing website level issues is to use WP_DEBUG and Query Monitor. Please check out our full article on how to use these tools to identify slow queries and/or PHP errors on your website:

WordPress Debug and Query Monitor

If you find that it’s a plugin, theme, or core functionality that’s the root cause of your issues, you can increase the time out length to see if this helps prevent 504s.

Increasing time outs is more of a band-aid than a genuine solution, however, it may help in the short term. This is a quick fix code snippet you can copy and paste into your server:

```
gp stack nginx -limits -client-body-timeout 600 && gp stack nginx -limits -client-header-timeout 600 && gp stack nginx -fastcgi -send-timeout 600 && gp stack nginx -fastcgi -read-timeout 600 && gp stack nginx -proxy -send-timeout 600 && gp stack nginx -proxy -read-timeout 600 && gp stack php 7.2 -max-exec-time 600 && gp stack php 7.3 -max-exec-time 600 && gp stack php 7.2 -max-input-time 600 && gp stack php 7.3 -max-input-time 600 && gp stack php 7.2 -max-input-vars 100000 && gp stack php 7.3 -max-input-vars 100000 && gp ngx restart && gp php 7.2 restart && gp php 7.3 restart && gp php 7.4 restart
```

Please see the final section of this article for the individual commands.

 

## 6. Check Your Website PHP Settings

### PHP INI Misconfiguration

This is rarely an issue, but sometimes see sites that are badly misconfigured – Max Execution Time and PHP memory limit, and other settings are excessively high.

PHP Memory Limit should only be higher than 256 if your website requires more memory than this. Other settings should generally not be higher than the defaults. This is a healthy set of PHP INI settings:

### PHP Worker Misconfiguration

If you’re experiencing long-running requests and you have too many PHP workers set for the available resources, you could be creating a backlog of tasks. This backlog can slow everything, including even simple requests, to a halt.

Open up your website’s customizer and click through to the PHP tab. Next, open the PHP FPM Settings tab and check your configuration. Below are our recommendations for each worker type.

###### Ondemand

Switch to Dynamic or Static.

###### Dynamic

For most websites, we recommend Dynamic with a minimum of one “PM Start Server” (active worker), and setting “PM Max Children” to 4 x CPU core (for example if you have a 1 CPU server, set it to 4, if you have a 2 CPU server, set it to 8 and so on). Below is a screenshot from a 2 CPU VPS:

If you’re still experiencing issues, try 3 x workers per CPU core.

###### Static

Static is better for more dynamic websites and ensures that you have workers active at all times, ready to process PHP. WooCommerce, LMS websites, and sites with lots of cache-bypassing traffic will benefit from static workers. If you’re experiencing timeouts, try adjusting this setting to 3 workers x CPU core. For example, the screenshot below is for a 2 CPU VPS:

If you’re still experiencing 504s you could reduce to 2 workers per core. This by itself will likely not fix your issue or be the root cause, but it will ensure you’re not pouring gas on the fire.

 

## 7. Check Your Access Logs

If your website is experiencing legitimately high traffic and it isn’t under attack, then you likely need a bigger server to handle the load.

### 1. Is your website under attack?

The quickest way to determine whether your website is under attack is to check the Nginx Error log and check the number of rate-limiting errors. If you’re being brute-forced, you’ll see something similar to following targeting either xmlrpc.php or wp-login.php:

```
[23/Apr/2020:16:23:43 +0000] 69.123.145.184 1.312 - yourwebsite.com "POST //xmlrpc.php HTTP/1.1" 200 413 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:23:46 +0000] 69.123.145.184 1.784 - yourwebsite.com "POST //xmlrpc.php HTTP/1.1" 200 413 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:23:48 +0000] 68.123.179.184 2.624 - yourwebsite.com "POST //xmlrpc.php HTTP/1.1" 200 413 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:23:52 +0000] 69.123.145.184 2.908 - yourwebsite.com "POST //xmlrpc.php HTTP/1.1" 200 413 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:23:55 +0000] 69.123.145.184 2.764 - yourwebsite.com "POST //xmlrpc.php HTTP/1.1" 200 413 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:23:57 +0000] 69.123.145.184 1.588 - yourwebsite.com "POST //xmlrpc.php HTTP/1.1" 200 413 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:23:59 +0000] 69.123.145.184 1.864 - yourwebsite.com "POST //xmlrpc.php HTTP/1.1" 200 413 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:29:55 +0000] 69.123.145.184 1.092 - yourwebsite.com "POST //wp-login.php HTTP/1.1" 200 6317 "https://yourwebsite.com//wp-login.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:29:57 +0000] 69.123.145.184 1.464 - yourwebsite.com "POST //wp-login.php HTTP/1.1" 200 6317 "https://yourwebsite.com//wp-login.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:29:59 +0000] 69.123.145.184 1.444 - yourwebsite.com "POST //wp-login.php HTTP/1.1" 200 6317 "https://yourwebsite.com//wp-login.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:30:00 +0000] 69.123.145.184 1.352 - yourwebsite.com "POST //wp-login.php HTTP/1.1" 200 6317 "https://yourwebsite.com//wp-login.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:30:02 +0000] 69.123.145.184 1.612 - yourwebsite.com "POST //wp-login.php HTTP/1.1" 200 6317 "https://yourwebsite.com//wp-login.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:30:05 +0000] 69.123.145.184 2.264 - yourwebsite.com "POST //wp-login.php HTTP/1.1" 200 6317 "https://yourwebsite.com//wp-login.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
[23/Apr/2020:16:30:06 +0000] 69.123.145.184 1.604 - yourwebsite.com "POST //wp-login.php HTTP/1.1" 200 6317 "https://yourwebsite.com//wp-login.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
```

If you’re not using XML RPC and it’s getting hit, you can disable it inside your website’s customizer. Open it up and then click through to the Security tab, and then to the additional measures. Click the XML RPC toggle.

If you’re not already using WPFail2Ban, you should activate this too.

### 2.1 Discover Attacking IPs on Nginx

Next, check your access logs on your server with the following commands. The first two will check for IPs hitting xmlrpc.php and wp-login.php, and the third will list IP accessing your server as a whole.

###### Check for hits on xmlrpc.php:

```
cat /var/log/nginx/*access.log | grep xmlrpc | awk '{print $1}' | sort | uniq -c
```

###### Check for hits on wp-login.php:

```
cat /var/log/nginx/*access.log | grep wp-login | awk '{print $1}' | sort | uniq -c
```

###### Check overall access for the day:

Here you’ll need to replace the date with the actual current date:

```
cat /var/log/nginx/*access.log | grep '11/Dec/2021' | sudo awk '{ print $1}' | sort | uniq -c | sort -nr
```

Here you may see some IPs with hundreds or thousands of hits on your website. If that’s the case, run this to display the top 50:

```
cat /var/log/nginx/*access.log | grep '11/Dec/2021' | sudo awk '{ print $1}' | sort | uniq -c | sort -nr | head -n 50
```

### 2.2 Discover Attacking IPs on OpenLiteSpeed

###### Check for hits on xmlrpc.php:

```
cat /var/log/ols/*access.log | grep xmlrpc | awk '{print $1}' | sort | uniq -c
```

###### Check for hits on wp-login.php:

```
cat /var/log/ols/*access.log | grep wp-login | awk '{print $1}' | sort | uniq -c
```

###### Check overall access for the day:

Here you’ll need to replace the date with the actual current date:

```
cat /var/log/ols/*access.log | grep '11/Dec/2021' | sudo awk '{ print $1}' | sort | uniq -c | sort -nr
```

Here you may see some IPs with hundreds or thousands of hits on your website. If that’s the case, run this to display the top 50:

```
cat /var/log/ols/*access.log | grep '11/Dec/2021' | sudo awk '{ print $1}' | sort | uniq -c | sort -nr | head -n 50
```

### 3. Ban Offending IP Addresses

The above commands may display a list like this:

```
root@ols-test-server:~# sudo awk '{ print $1}' /var/log/ols/*access.log | sort | uniq -c | sort -nr | head -n 101333 "94.137.186.125399 "1.46.145.212349 "107.150.94.78336 "54.93.217.201333 "122.155.174.174195 "185.70.52.218139 "185.225.234.17492 "185.225.234.5988 "185.225.234.19965 "1.46.4.227
```

You can block these IP’s by running the following command on your server:

```
ufw deny from {IP.Address}
```

For example:

```
ufw deny from 199.199.199.19
```

### 4. Mitigate Attacks with Cloudflare

If you’re using Cloudflare or have a security plugin such as WordPress you can add these IP’s to your blacklist, but you’ll also want to check out our Fail2Ban article here:

Configuring Fail2Ban to Prevent Brute Force Attacks

And if you’re not already on Cloudflare, consider a move there and activate DDOS protection. You can enable I’m Under Attack mode via the following steps:

 

## 8. Has Your Site Been Compromised?

If your website has been hacked, this may be wreaking all kinds of havoc on your site and server. If you’re on our developer plan, we can install and run Malware detection software for you, and/or there are great WordPress security plugins that can scan your website for free such as Wordfence and Sucuri.

If you have been hacked, please check this article:

Moving a Website that’s had a Malware Infection

 

## Further Troubleshooting Steps if CPU Usage is NOT High

### 1. Clear your cache, wait a minute or two and retry

If all looks healthy in Monit, then it may just have been a very brief outage that has now self-corrected. It’s also possible this was caching related, and a full cache clear via the self-help tools may remedy the issue immediately.

There’s no such thing as perfection 24/7. Sometimes a brief glitch may occur on one of your servers – unlikely as it may be – and it will quickly return back to normal. This may simply be a one-time thing, so continue to recheck your website for the next few minutes. If you notice it occurring frequently, then something deeper is likely happening.

### 2. Determine if this is actually a website/server issue or a CDN/Firewall/Proxy Issue

If your server is all green or doesn’t look like it should be experiencing time out issues, then it may be that neither the server nor website is at fault at all, and it may either be your CDN, DNS level firewall, or proxy server that are slowing things down.

Try deactivating these one by one so you can connect to your server directly without interference.

### 3. Clone to staging, shut plugins down in staging environment, reactivate one by one

This is a natural follow-on to #2 above. If you’re struggling to identify the cause of your slow load times, clone your site over to a staging environment, switch to a default theme, and deactivate all of your plugins. You now have a baseline to work with and can start activating your plugins one by one, and then your theme until you identify the root cause.

 

## Fixing WordPress Login / WP-Admin 504 Errors / Upload Timeouts

These issues indicate an inefficient codebase.

The following settings can be adjusted to help fix your issue for the short term – especially if you’re simply uploading a file – but these are a band-aid that can help you diagnose and fix your website, not a solution.

### Nginx Helper Settings

On Nginx servers, make sure the cache setting in the Nginx Helper plugin inside your site is set correctly so that it matches the cache setting in the UI. If Redis is active in the UI but the plugin is set to FastCGI (or vice versa) you may experience strange behaviour that could include 504 timeouts.

### Adjusting PHP

To begin, you can first try adjusting your PHP settings. Here you can begin by changing the settings from the defaults to the follow:

### Adjust Nginx

Next, adjust the following Nginx settings. For this, you will need to SSH into your server – please see the guides listed in Part 4 above.

Run each of the following commands below.

#### Client Body Timeout

Default: 30

```
gp stack nginx -limits -client-body-timeout 600
```

Learn more here.

#### Client Header Timeout

Default Setting: 30

```
gp stack nginx -limits -client-header-timeout 600
```

Learn more here.

#### FastCGI Send Timeout

Default Setting: 60

```
gp stack nginx -fastcgi -send-timeout 600
```

Learn more here.

#### FastCGI Read Timeout

Default Setting: 60

```
gp stack nginx -fastcgi -read-timeout 600
```

Learn more here.

#### Proxy Send Timeout

Default Setting: 60

```
gp stack nginx -proxy -send-timeout 600
```

Learn more here.

#### Proxy Read Timeout

Default Setting: 60

```
gp stack nginx -proxy -read-timeout 600
```

Learn more here.

### Next Steps

If the above still doesn’t work you could also try adjusting your connection timeout settings and keep connection alive settings.

After that you will need to identify the root cause, which may mean switching on WordPress debug and query monitor, and then deactivating plugins one by one and switching to the default WordPress theme.

Once you know where the source of the issue is you can set about fixing it, or replacing it with a different solution.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

