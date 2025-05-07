# Diagnosing HTTP 500 / Internal Server Errors | GridPane

# Diagnosing HTTP 500 / Internal Server Errors

 

8 min read 

### Table of Contents

 

## Introduction

500 errors can be caused by a variety of different factors, but by far the most common reason is errors within the codebase of your website.

There’s usually either a fatal error due to a PHP conflict, PHP error, or a lack of PHP memory due to a plugin needing above 256M to function correctly (more common on the backend than the frontend). This is the issue 99% of the time.

The messaging that displays with your 500 error may vary, but the variations don’t indicate any specific issues. Here are a few common examples:

### But My Codebase Hasn’t changed?

If you’re keeping your website up-to-date, your codebase regularly changes, even if you aren’t adding new plugins. Updates can cause conflicts, and plugins can require more memory. Sometimes uninstalling a plugin can cause issues, and then there’s the possibility that malware has caused some damage to your codebase.

### 500 DEBUG

Below are our recommended steps, in order (check each section one after the other), to diagnose your 500 errors by quickly narrowing down the root of the cause.

Some of these checks may require you to connect to your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Quick Checks

There are a few checks you can run to make sure it’s not a simple issue at the root of your 500 error.

### 1. Check Your Spelling and DNS Records

These will seem silly, but we have seen these happen in support on far too many occasions to not include.

First, double-check that you have spelled the domain name correctly.

Second, check that your website’s DNS is incorrect. We recommend this website: https://dnschecker.org/#A

If using Cloudflare you can use a local redirect to connect to the website directly and confirm the IP in the response headers, or quickly disable the proxy and use the website to confirm before switching the proxy back on.

### 2. Check the Website Without the Cache

First, check the website in an incognito window to rule out the browser cache. Clear your browser cache and cookies if the website now works correctly.

If that isn’t the cause, check the website when bypassing the cache (simply add a query string like ?123 to the end of your UR, e.g. website.com?123). If the website now works, clear your cache.

### 3. Reset Your Websites Permissions

If you’ve made any changes to your installation manually, you may have changed/set the ownership of those files to the root user instead of the system user.

When this happens, your website doesn’t have the correct permissions to access the files.

Head to the Tools page inside your GridPane account and do the following:

### 4. Rename the /plugins directory

Connect to your server over SFTP and rename the plugins folder inside /wp-content to plugins.off. Does this fix the issue? If yes, you now know that the issue is specific to a plugin in your website. Change the folder name back to plugins and you can start narrowing it down by following the same process for each of your individual plugin folders.

You may want to start with the plugins you have the least confidence in.

 

## PHP Service Checks

If there’s an issue with PHP on your server, this can cause 500 errors.

### 1. Check if PHP is Down

If PHP is down, Monit will have tried to alert you, but the quickest way to check is to head to your Servers page inside your GridPane account and click the piechart icon next to your server to open up Monit.

If you see that any PHP version is down, click on its name and you will be able to attempt to restart it at the bottom of its page.

Alternatively, on the command line you can run the following:

```
gp php {php.version} -restart
```

For example:

```
gp php 7.3 -restart
```

### 2. If PHP is Down and Won’t Restart

Switch your website to another PHP version, then contact the support team and let us know which specific PHP version is down and that it won’t restart. We’ll look into the issue.

 

## Codebase Checks: PHP and WordPress

The most common cause of a 500 error is a fatal error within the website either due to a PHP error or a lack of PHP memory.

PHP errors can be caused by many things, including missing files and malware. The website Nginx/OpenLiteSpeed Error Logs are where you need to check.

### 1. Check the Nginx error log

You’ll find all of your website-specific error logs inside your website’s customizer. Head to the Sites page within your account and click on the name of the website you’re having trouble with to open the customizer. Next, click through to the logs tab:

You’ll find the Nginx error log at the bottom:

When checking the log, look for the errors that correspond to your timestamps.

### 2. Are there any Fatal Errors?

If yes, it will tell you whether it’s due to it being a PHP error or a lack of memory. If it’s a codebase error you will need to fix the error to resolve the issue. This may mean deactivating the plugin, or diving into PHP.

If the error is only happening on one page, or when doing something in the WordPress backend, also activate WordPress debug with the toggle at the top of the logs tab.

#### Check the following:

A common cause is a lack of PHP memory, which you can increase directly inside your website’s customizer.

### 3. Did the 500 Error Occur after activating or deactivating a plugin?

If things went wrong after a plugin activation, deactivate the plugin (manually if necessary by connecting to your server over SFTP or SSH and renaming the plugins folder).

If things went wrong after a plugin deactivation, try restarting PHP.

### 4. Are all WordPress installation files OK?

Check that your website core files aren’t missing or corrupted – a missing or misplaced file can cause 500 errors.

You can run a check with the following command (replace site.url with your domain name):

```
gp wp site.url core verify-checksums
```

For example:

```
gp wp yourwebsite.com core verify-checksums
```

This will check your core WordPress installation files and let you know if there are any issues that need to be addressed.

We rarely see 500 errors, but this is often the cause. A few examples we’ve seen are:

 

 

### wp-config.php backup

If you find that for some reason your wp-config.php is missing/corrupt/empty, you can find a backup of this file inside /opt/gridpane/site-configs.

### 5. Scan for Malware

If things look out of place, files are missing, or the above command returned that core files were incorrect, then you should check your website for malware.

If you’re on the Developer plan we can activate the Maldet scanner for you (contact us on support). WordPress scanners such as MalCare, NinjaScanner, and Wordfence can be great options as well.

 

## OpenLiteSpeed Specific Checks

There are a couple of checks that are OpenLiteSpeed specific.

### 1. Check Your .htaccess File

If the .htaccess file is missing, corrupted, or misconfigured, it can cause 500 errors. There is a backup of your original .htaccess file inside your /htdocs directory called .htaccess.bk.

### 2. Deactivate the LiteSpeed Cache Plugin

Does deactivating the LiteSpeed Cache plugin resolve the issue?

Previously we diagnosed a very obscure error within OpenLiteSpeed itself that resulted in a 500 error due to the LiteSpeed Cache plugin.

 

## Database Checks

Database issues are very rarely the cause of 500 errors, but if you’ve confirmed the issue isn’t any of the issues detailed in the previous two sections, you can make the following checks.

### 1. Incorrect Database Credentials

Incorrect database credentials in your websites wp-config.php file could potentially cause a 500 error.

Check your original database credentials with either of the site.env file:

```
/var/www/site.url/log/site.url.env
```

Or the wp-config.php backup:

```
/opt/gridpane/site-configs/site.url-wp-config-immutable.BUP
```

Do they match up with your current wp-config.php file?

### 2. There are Issues with your database server

Check Monit to see if MySQL up and running. If MySQL is down, you can attempt to restart it. If it doesn’t restart, contact us on support.

### 3. Corrupted database

Connect to your server over SSH, and check your database with the following command (replacing site.url with your websites domain):

```
gp wp site.url db check
```

If there’s an issue, you can attempt to run a repair with the following (again replacing site.url with your websites domain):

```
gp wp site.url db repair
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

