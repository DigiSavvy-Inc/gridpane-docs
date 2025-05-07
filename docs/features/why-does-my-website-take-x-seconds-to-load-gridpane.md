# Why Does My Website Take X Seconds to Load? | GridPane

# Why Does My Website Take X Seconds to Load?

 

4 min read 

## Introduction

A question we sometimes see is why a website is experiencing slow page load times. Sometimes this is a specific page on the website. Other times it’s the website as a whole that’s slow to respond.

This article offers some insights and guidance into why this may occur and where to begin troubleshooting. Most of the troubleshooting steps for this kind of issue are the are same as debugging a 504 error which you can learn more about here:Diagnosing 504 Timeouts and Performance Issues

### Table of Contents

 

## Common Reasons for Experiencing Slow Page Loads

The following are the most common reasons for experiencing slow page loads:

It’s also possible your website is under attack or has been compromised, but that’s a lot less likely.

The first 5 are pretty quick to rule out:

Issues 6-9 require some debugging.

 

## Check for Database Table Locking

Table lock is one of the most common causes behind both 502 and 504 errors, and also slow load times in general. To check for table locking you will need to connect to your server via SSH as the root user. Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

You can check to see if you have any locked tables by first running:

```
gp mysql login root
```

And then run:

```
show processlist;
```

If you see “Waiting for table metadata lock”, you’re experiencing table locking.

Exit MySQL with:

```
exit
```

### How to Fix it

You can fix this by restarting MySQL with the following command:

```
gp mysql restart
```

You can also restart MySQL inside of Monit as well

 

## Basic Plugin Debug

You may find that after steps 1 and 2, you don’t need the other steps, but deactivating plugins one by one is a reliable way to find where you have bottlenecks in your codebase.

### Step 1. Check Your Error Log

You can find your website error log inside your website customizer in the logs tab. Here you may be able to quickly see that a specific plugin is causing errors.

### Step 2. Enable WP Debug

The best way to begin diagnosing website-level issues is to use WP_DEBUG and Query Monitor. Please check out our full article on how to use these tools to identify slow queries and/or PHP errors on your website:

WordPress Debug and Query Monitor

### Step 3. Clear the cache and recheck

You can get a real picture of performance when you clear the cache and then test your website bypassing the cache. You can bypass the cache by adding a query string to the end of your URL, for example, mywebsite.com/?123.

Use GTMetrix to take a scan of the site while bypassing the cache, and record those results. This will be your baseline, and it’s important to look at the waterfall. It can be anything from external assets, to plugins causing this delay.

### Step 4. Disable all plugins

Run a new GTMetrix scan once disabled. This will give you a picture of what the maximum performance might could be.

You could do this on your staging website instead of on the live website.

### Step 5. Re-enable Plugins One by One

Retest until you find the source. You can measure in between enabling plugins. By testing each one, you can see which plugin is adding the most time.

 

## PHP and MySQL Slow Logging

Enabling your websites PHP slow log and server MySQL can help you identify bottlenecks that are causing your site to run slow, and then fix them.

### PHP Slow Logging

By identifying the specific PHP requests that are running slow, you can set about either fixing the code itself or replacing the plugin responsible for the bottleneck (it’s almost always a plugin). Learn more here:Using the PHP Slow Log

### MySQL Slow Logging

MySQL slow query logging can be a highly useful tool for uncovering performance bottlenecks in your websites.

The MySQL slow query log is where the MySQL database server will log all queries that exceed a time (in seconds) that you specify. This can be particularly helpful on database-intensive websites, such as WooCommerce stores. Learn more here:Using the MySQL Slow Log

 

## Additional Troubleshooting Guides

Here are a couple more guides related to performance:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

