# Diagnosing Migration Issues | GridPane

# Diagnosing Migration Issues

 

20 min read 

 

### Information

This article contains a wealth of information that can help you become an expert on migrating WordPress websites from one place to another. Please be sure to make it your first stop if you ever experience an issue.

## Introduction

This article details some of the reasons why migrations sometimes don’t go smoothly. If you’ve had issues migrating a site over, this should serve as a good guide to begin diagnosing the issue.

###### The most common issues we see are as follows:

###### Known issues when migrating from specific hosts:

###### Plugin, PHP, and other issues:

### Connecting to Your Servers

Some of the following may require you to SSH into your server. Don’t worry, almost anything you may need to do via SSH by following articles here in our knowledge base is the equivalent of basic HTML difficulty-wise. Please see these guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Force SSL plugin / Forced HTTPS

###### The Problem

You’ve migrated your website in, but keep getting either redirected or taken to /signon.php and says “Your session was finished.”

###### Diagnosis

If you’ve migrated a website that has the Force SSL plugin installed and activated, but you don’t have an SSL certificate on GridPane, you will not be able to access your website. The same goes for if your website is all set up for HTTPS but doesn’t have an SSL certificate.

###### The Solution

Provision an SSL for your website, and your website will function correctly.

 

## Incorrect Database Table Prefix

###### The Problem

You’ve imported your site, but all the plugins are deactivated, and content is missing.

###### Diagnosis

We sometimes see this when migrating from managed hosts such as Kinsta and WP Engine. Here you need to check to see if the database table prefix is “wp_”. You can do this by clicking on the database icon next to your website to open up phpMyAdmin:

We’re looking to see if these match up (be sure to check thoroughly, as the original database tables from the site’s creation may still be there):

A custom prefix could potentially be anything, but often looks something like: “wp87f_“

###### The Solution

If your table prefix doesn’t match up, but all your database tables are using the same prefix, you can edit the table prefix in your wp-config.php via SFTP (download, edit, re-upload) or the command line.

To edit via the command line type the following command (switch out “site.url” with your domain name):

```
nano /var/www/site.url/wp-config.php
```

Edit your prefix, and then hit Control+O, and then enter to save the file. Exit with Control+X.

 

## Strange Behaviour/Redirects: Check for Two Competing wp-config.php Files

If things aren’t working the way they’re supposed to after migrating, and the above issues aren’t the cause, make sure that there isn’t a second wp-config.php file inside your websites /htdocs folder.

GridPane securely stores the wp-config.php file 1 level up outside of /htdocs here:

```
/var/www/site.url
```

If you have two wp-config.php files – 1 in the correct place, one in /htdocs – these can interfere with each other and cause problems. Please simply delete the wp-config.php file inside /htdocs if it exists, and leave ours in its place.

You can do this either by connecting to your server by SSH (links at the beginning of the article), or by connecting to your server over SFTP:

Connect to a GridPane Server by SFTP as Root user

To  delete them directly on your server,

you can navigate to your website htdocs folder with the following command (switching out “site.url” for your websites domain name):

```
cd /var/www/site.url/htdocs
```

Then display the contents of the file with:

```
ls -l
```

And if you see a wp-config.php file, you can rename it with:

```
mv wp-config.php wp-config.php_off
```

Or you can delete it with:

```
rm wp-config.php
```

Once that’s done, recheck your website.

 

## Are Must-Use Plugins Breaking Your Site?

###### The Problem

A common issue we see is that plugins installed by the previous host result in critical errors, sometimes breaking the site entirely. Sometimes they can make a site extremely slow, or result in other PHP errors.

This is a very common practice nowadays. If migrating a site from GridPane to another platform, you will also want to remove our must-use plugins first as well.

###### Diagnosis

Normally, these are installed as Must-Use plugins, and they can be found inside:

```
/var/www/site.url/htdocs/wp-content/mu-plugins
```

(The above is the GridPane directory structure). This can be accessed by SSH or SFTP.

A quick way to test if this will fix your website is to rename this folder temporarily and retest your site.

###### Solution

If the issues you were seeing on your website are now resolved, you can leave this folder in its renamed state for the moment so that you have all the plugins for reference. Once you know what you need and what you don’t, you can remove the ones you don’t need entirely.

 

## Migrating from Kinsta, WPEngine, or Cloudways

There are a couple of things to be aware of when migrating from these 3 hosts to another host:

### Your Website Looks Broken / Like a Brand New WP Site

###### The Problem

You’ve migrated your website over, but it either appears broken, or you’re still seeing a default WordPress installation.

###### Diagnosis

Kinsta, WPEngine, and many other managed WordPress hosting companies add a custom table prefix to their databases. If all your plugins have been installed on your site, but none are active, this is likely to be the cause.

If your website appears to be broken entirely, then this may be due to a must-use caching plugin, or other must-use plugins.

###### The Solution

If your plugins are all inactive, click here to go to the “Incorrect Database Table Prefix section”.

If your site appears broken, connect to your server (either by SFTP or SSH) and remove the plugin. As this is stored in the wp-content/mu-plugins/ directory, it cannot be uninstalled from the WP dashboard.

### Plugins aren’t working / Critical or Fatal Errors

###### The Problem

Must-use plugins are still installed on your site but don’t work outside of their original hosting environment.

###### The Solution

Connect to your server over SFTP, navigate to /wp-content/mu-plugins, and delete or move the plugins. See this section for more details.

 

## Migrating from Flywheel

There are a couple of things to be aware of when migrating from Kinsta to another host:

### Your Website Looks Broken / Like a Brand New WP Site

###### The Problem

You’ve migrated your website over from Flywheel, but you’re still seeing a default WordPress installation (or simply just not seeing the correct website).

###### The Solution 1.1

Local by flywheel use: short_open_tag by default. Here at GridPane, we have this closed by default. To get your website up and running, we’ll need to activate short_open_tag.

You can do this directly inside your site customizer. First, head to your Sites page inside your account and click on your website’s domain name. This will open up the customizer.

Next, click through to the PHP tab, and toggle on Short Open Tag, as shown in the image below:

###### The Solution 1.2

If that doesn’t work, check your database table prefix as detailed in this section.

### There has been a critical error on your website

###### The Problem

Every page on your website is reporting a critical error, and the migrated website isn’t working.

###### Diagnosis

Check your Nginx error logs. Are you seeing the following errors?

 

```
2021/07/14 12:26:23 [error] 1495#1495: *31 FastCGI sent in stderr: "PHP message: PHP Warning: Use of undefined constant FLYWHEEL_PLUGIN_DIR - assumed 'FLYWHEEL_PLUGIN_DIR' (this will throw an Error in a future version of PHP) in /var/www/example.com/htdocs/.fw-config.php on line 12PHP message: PHP Warning: require(FLYWHEEL_PLUGIN_DIR/flywheel/flywheel-core.php): failed to open stream: No such file or directory in /var/www/example.com/htdocs/.fw-config.php on line 12PHP message: PHP Fatal error: require(): Failed opening required 'FLYWHEEL_PLUGIN_DIR/flywheel/flywheel-core.php' (include_path='.:/usr/share/php') in /var/www/example.com/htdocs/.fw-config.php on line 12" while reading response header from upstream, client: 94.137.186.125, server: example.com, request: "GET / HTTP/1.1", upstream: "fastcgi://unix:/var/run/php/php74-fpm-example.com.sock:", host: "example.com"
2021/07/14 12:26:24 [error] 1495#1495: *31 FastCGI sent in stderr: "PHP message: PHP Warning: Use of undefined constant FLYWHEEL_PLUGIN_DIR - assumed 'FLYWHEEL_PLUGIN_DIR' (this will throw an Error in a future version of PHP) in /var/www/example.com/htdocs/.fw-config.php on line 12PHP message: PHP Warning: require(FLYWHEEL_PLUGIN_DIR/flywheel/flywheel-core.php): failed to open stream: No such file or directory in /var/www/example.com/htdocs/.fw-config.php on line 12PHP message: PHP Fatal error: require(): Failed opening required 'FLYWHEEL_PLUGIN_DIR/flywheel/flywheel-core.php' (include_path='.:/usr/share/php') in /var/www/example.com/htdocs/.fw-config.php on line 12" while reading response header from upstream, client: 94.137.186.125, server: example.com, request: "GET /favicon.ico HTTP/1.1", upstream: "fastcgi://unix:/var/run/php/php74-fpm-example.com.sock:", host: "example.com", referrer: "https://example.com/"
```

###### The [Quick] Solution

Connect to your server over SFTP or SSH and delete the file from your htdocs directory. That should get your website back up and running.

Contact Flywheel for instructions on how to disconnect your websites from their platform (and ask them why they do things this way too…).

 

## Layered Caches

###### The Problem

You’ve migrated your website in but it looks broken.

###### Diagnosis

If you visit your website before the migration is complete, it could cache the partially created website, which could result in a layered cache, essentially breaking your website on the front end.

###### The Solution

Clear your website’s cache via the website customizer caching tab, or using the self-help tools inside your GridPane account:

 

## OpenLiteSpeed Syntax Errors After Migration

###### The Problem

You’ve migrated your website in, but now you’re getting OLS syntax error notifications.

Note that if you’re getting errors after importing, but you weren’t getting them before, then the issue is specific to the website you’ve imported and you will need to debug your website to fix the issue.

###### Diagnosis

A plugin in your website is likely writing to your .htaccess file, but it’s added code that has resulted in a syntax error.

###### The Solution

Check your .htaccess file for anything specific to the plugins in your website and remove it.

Next, restart and regenerate the website configuration with this command (replace “site.url” with your domain name):

```
gpols site site.url
```

 

## PHP Short Open Tag

###### The Problem

If your website uses PHP short open tag, then when you first migrate into GridPane, you may see a fresh WordPress install vs your actual website

###### Diagnosis

If all your website’s files and folders are there, and the site is still showing a default installation or default theme after clearing the cache via the self-help tools.

###### The Solution

The solution is to activate “Short Open Tag” inside the PHP INI Settings tab. Full details can be found above here the Flywheel section.

 

## PHP Version

###### The Problem

You’ve migrated your website into GridPane, but it’s throwing PHP errors and isn’t working the way it should – or isn’t working at all.

###### Diagnosis

If you’re bringing an old website over to GridPane from a “low-quality host,” it may not be compatible with up-to-date (and secure) versions of PHP. Check the previous web host to see what PHP version your website was running on. It’s possible they may still be using PHP 5.6 or below, none of which are currently supported.

###### The Solution

First, check if the website is as up-to-date. Any plugin or theme that is regularly maintained/updated will be compatible with supported versions of PHP. Updating everything may fix your issue.

If this doesn’t help, you may need to replace the outdated plugin/s and/or theme, and you could either do this on your own computer or previous host.

 

## PHP Execution Time

###### The Problem

While trying to migrate your website into GridPane, the process is timing out and causing the migration to fail.

###### The Solution

There are two things you’ll want to look at here. The first is PHP execution time. The second is to make sure no request terminate timeout is set in the pool.d site conf.

First, you will need to SSH into your server. Please see the guides listed at the start of this article to get started.

### Set the maximum execution time for a site’s PHP script.

The following commands will set the maximum time in seconds a site’s PHP script is allowed to run before it is terminated by the parser.

Directive: max_execution_timeUnit: SecondsDefault value: 600

```
gp stack php -site-max-exec-time {integer} {site.url}
```

Example:

```
gp stack php -site-max-exec-time 1200 gridpane.com
```

### Check the pool.d site config

By default, this isn’t set, so if you (or a developer of yours) haven’t edited this in the past, you won’t need to worry about checking your site config here. If you have edited it, or simply aren’t sure if you or another member of your team may have, you can check with the steps below.

First, check your website’s PHP version:

Next, open up your websites pool.d site config with the following command, replacing {php.version} and {site.url} with your PHP version and websites domain:

```
nano /etc/php/{php.version}/fpm/pool.d/{site.url}.conf
```

Example:

```
nano /etc/php/7.4/fpm/pool.d/gridpane.com.conf
```

Inside nano, press Control+W to open up the search, and paste:

```
request_terminate_timeout
```

and hit enter.

This will bring you to the correct line. In the image above, this has been commented out, which means there’s no limit.

If you have a limit in place, need to edit the number at the end of this line. By default, it’s set to:

```
request_terminate_timeout = 900
```

900 means 900 seconds. You increase the length of the timeout so that your import is successful. You can then change this back once you’ve completed migrating your website over.

To save the file, hit Control+O, then enter. To exit nano, hit Control+X.

 

## Incorrect Database Credentials

###### The Problem

You’ve migrated your website into GridPane, but you’re experiencing an “Error Establishing a Database Connection” or 504 timeouts.

###### Diagnosis and Solution

Here we want to check the following things:

To begin your diagnosis, please refer to the credentials/table prefix section of our database troubleshooting article:

Diagnosing and Fixing: “Error Establishing a Database Connection”

 

## Wordfence

We see Wordfence interfere with migrations somewhat regularly. We even have a dedicated article on the problem on the topic here: Disabling Wordfence completely before migrating

###### The Problem

Your migration won’t complete, your website isn’t functioning correctly, or you’re seeing a 500 critical error.

###### Diagnosis

Is WordPress activated on the site you’re trying to migrate over? And is there a hardcoded path inside the .user.ini file? If yes, this may well be breaking your website.

###### The Solution

First, try deactivating and re-activating Wordfence – you may need to do this by renaming its folder name inside the plugin’s directory via SFTP.  Additionally, Wordfence often adds a hardcoded path to the .user.ini and wordfence-waf.php files (located in your website’s htdocs folder), and if you move from one environment to another, it can result in a 500 error (critical error).

Either adjust the hardcoded path or simply remove the Wordfence content from the file. If neither of these gets your website up and running, you may need to try the migration again but with Wordfence deactivated.

 

## ManageWP

###### The Problem

You’ve migrated in using ManageWP, but your website isn’t loading or is redirecting to another domain on your server, or is totally broken.

###### Diagnosis

We’ve seen ManageWP have some bizarre results when migrating into GridPane.

###### The Solution

Unfortunately, there isn’t a good solution for most of the above.

Always make sure you have caching disabled before migrating, as we’ve seen this cause multiple issues, including fatal errors.

Ideally, you need to copy our wp-config.php, then once ManageWP has replaced ours, you switch the original back in again.

You can also use a different migration solution, such as All in One WP Migration or Migrate Guru. Neither of which will replace things they shouldn’t be replacing.

 

## Duplicator

###### The Problem

You’ve migrated your website into GridPane using Duplicator, but your website isn’t loading or is totally broken.

###### Diagnosis

Duplicator is a great plugin, but unfortunately, because we store the wp-config.php outside of htdocs, using it on GridPane can cause problems.

###### Solution

You may be able to recover your original wp-config file, but it may be easier to simply be easier to migrate your website again using a different plugin. We recommend All in One WP Migration and Migrate Guru as these work exceptionally well with our platform.

To access a backup of your wp-config.php file by SSH’ing into your server and running the following command (switch out “site.url” with your domain name):

```
nano /opt/gridpane/site-configs/site.url-wp-config-immutable.BUP
```

Example:

```
nano /opt/gridpane/site-configs/gridpane.com-wp-config-immutable.BUP
```

Here you can copy the contents and add the correct details to your website’s wp-config.php file.

 

## “Failed to Connect to FTP Server” Error

If you’ve migrated a website over to GridPane but you’re being asked for S/FTP credentials when trying to install a plugin or theme (or maybe even run updates), this means that your file/folder permissions will be incorrect.

### How To Fix It

First, visit the Tools section by clicking the link in the main menu:

You will see the quick fix panel at the top of the main window:

GridPane will check all directory and file permissions to make sure they’re all correct. This tool is particularly useful when there are errors or other strange behavior coming from your site.

 

## Website “Downloads” Instead of Loading in the Browser After Migration

###### The Problem

If you’re trying to access your website, but instead it downloads instead of loading in the browser, the issue is caused by the GZIP compression being enabled twice.

###### The Solution

Deactivate any plugin-based GZIP. WP Rocket is the likely candidate if you have this installed on your website. Also, if you’ve migrated from Apache, OpenLiteSpeed, or LiteSpeed, you may need to remove this from your .htaccess tool.

Full details on how to troubleshoot this issue can be found in this article:

Why Does My Website “Download” Instead of Load? Double Gzip and How to Fix it

 

## Beaver Builder Cache

Note: This was reported to us, but we’ve been unable to replicate the issue.

If cloning a site that uses Beaver Builder, it’s possible it may clone direct file paths across in the cache. Please clear your Beaver Builder cache if such issues occur, and you could also try clearing the cache before you clone your website. If the issue persists, you will need to manually delete the cache folder from the server. Beaver Builder says this on their FAQ page:

I migrated a site but my image URLs didn’t change. How do I clear the Beaver Builder cache?

If you’re having trouble after migrating a site (make sure you use a Serialized Search & Replace tool) you probably need to clear Beaver Builder’s cache. You’ll need to locate Beaver Builder’s cache folder. You can find this in your wp-content/uploads folder in either the fl-builder/cache or bb-plugin/cache folder depending on your install. Remove the cache folder and that’s it!

Quoted from the Beaver Builder FAQ Page.

 

## UpdraftPlus

UpdraftPlus is a great plugin and generally works very well with GridPane. If you’re finding that your migrations are resulting in slow response times, and/or are partly broken, the following will help you get started troubleshooting.

### Step 1. Disable Caching, Firewalls, Proxies

UpdraftPlus specifically recommend the following for migrating one site to another:

“By the way – before you begin, try to turn off any proxies that are between you and your site, such as Cloudflare, GoDaddy’s “Preview DNS” proxy, or Opera Turbo/Road mode. These can get in the way. Also, cacheing and minifying plugins are a possible cause of migration problems (whatever method you use). If possible, disable all of those before you create your backup – or alternatively, just be ready to turn them off if the migration stumbles.”

https://updraftplus.com/faqs/how-do-i-migrate-to-a-new-site-location/

Firewalls could also potentially result in errors during the import as well.

### Step 2. Test your migration without the “Others” Folder

When importing your site, it’s possible that something inside the “Others” folder will cause things to go wrong. We highly recommend ruling this option out before moving on to step 3.

You can check your Nginx Site Error log for more information on whether this is likely to be the issue. After importing your website with the “Others” folder, go to your GridPane account and navigate to the Sites page. Then click on your website to open up the configuration modal, and click through to the logs tab. You will see the Nginx Error log at the bottom:

#### Plugins

If you narrow down things to a specific plugin (for example, we had a case where “Nobuna” was causing some major issues via the “Others” folder when migrating in), you can first try deactivating the plugin before migration or, depending on the plugin and it’s data, uninstall and then reinstall it once the site has been migrated across.

### Step 3. Enable SUPER Permissions

During some of our own extensive testing, the only thing we were able to flag was a SUPER permissions error. In our case, this didn’t result in any noticeable errors in our test sites, but it is possible that this could result in errors for some WordPress sites.

To enable SUPER permissions on your website, please see our guide here:

How to Grant SUPER Permissions for Your Website

 

## Rocket-Nginx Caching

###### The Problem

If you’ve set up Rocket-Nginx caching for your websites (WP Rocket and Rocket-Nginx Caching on GridPane), you will get an Nginx syntax error if you don’t first set up Rocket-Nginx on the destination server, or remove the /var/www/site.url/nginx/rocket-main-context.conf from your website before migrating.

The error will look as follows:

```
root@server-name:~# nginx -t
nginx: [emerg] open() "/etc/nginx/rocket-nginx/default.conf" failed (2: No such file or directory) in /var/www/site.url/nginx/rocket-main-context.conf:2
nginx: configuration file /etc/nginx/nginx.conf test failed
```

###### The Solution

Remove Rocket-Nginx caching from your website before migrating, OR, set up Rocket-Nginx on your destination server before migrating.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

