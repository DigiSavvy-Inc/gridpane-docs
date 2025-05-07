# Additional Security Measures: WordPress Website Hardening for Nginx and OpenLiteSpeed (OLS) | GridPane

# Additional Security Measures: WordPress Website Hardening for Nginx and OpenLiteSpeed (OLS)

 

11 min read 

### Table of Contents

The following WordPress hardening options will allow you to configure individual websites on an as-needed basis to easily increase their security.

This includes blocking xmlrpc.php, load-scripts.php, PHP executing in wp-content, block comments, block links OPML, block trackbacks, and block the wp-admin upgrade and install file.

These commands block these at the webserver (Nginx/OpenLiteSpeed) level, which means requests are blocked by the server before they have chance to hit your website.

 

## The Additional Measures Tab

All of the following GP-CLI below can now be toggled ON and OFF directly inside your website’s configuration modal. These toggles will run the activation GP-CLI when toggled ON, and they will run the deactivation GP-CLI when toggled OFF.

By default, all settings are toggled off, unlike Fail2Ban and the Web Application Firewalls (WAFs). The reason for this is that these are their own individual measures, and they aren’t individual rulesets of a singular specific security feature.

### Activation

To activate these settings, head to the Sites page inside your GridPane account and then click on the website that you wish to configure:

This will open up the website customizer modal. Next click through to the Security tab, and then the Additional Measures tab:

As pictured above, here you will find a toggle for each of the individual settings detailed in this article.

We highly recommend you read up on what each one does below and incorporate them into your security routines as appropriate. You do not need to run the GP-CLI commands if you are using the toggles inside your GridPane account.

 

## SSH into your server

To run them, you will need to SSH into your server. See the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Enable/Disable XML RPC

WordPress has a file named xmlrpc.php. It’s really a legacy feature that allowed you to login and interact with your site by remote, enabling data to be transmitted, with HTTP acting as the transport mechanism and XML as the encoding mechanism. It was the WordPress API before the REST API, except far less useful or secure.

And in recent years it has become a real pest – being the primary target for malicious Bots to overload your server.

By default, XML-RPC is active on your WordPress sites. If you aren’t using it, you should disable it, but if you do this at the WordPress level only, then your server can still be overloaded with requests that go nowhere. Instead, let’s drop it at the server level.

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/disable-xmlrpc-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/disable-xmlrpc-main-context.conf
```

Which contains configurations to:– Deny Access to the xmlrpc.php– Removes the X-Pingback header that WordPress adds

### GP-CLI Commands

Disable XML-RPC with:

```
gp site {site.url} -disable-xmlrpc
```

Enable it again with:

```
gp site {site.url} -enable-xmlrpc
```

 

## Enable/Disable Concatenating Load Scripts

WordPress has a feature that concatenates WP-Admin JS and CSS. While this may seem innocuous there are circumstances where this could be used to DoS a server, and in the age of HTTP/2 multiplexing, it isn’t really necessary.

NOTE: On a small handful of websites, this sometimes breaks the wp-admin area, displaying it as unstyled HTML.

More details can be found regarding CVE-2018-6389 here.And a nice article by Bjørn Johanse regarding it here.

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/disable-load-scripts-concatenation-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/disable-load-scripts-concatenation-main-context.conf
```

Which contains configurations to:– Deny access to ../wp-admin/load-scripts.php– Deny access to ../wp-admin/load-styles.php

It also defines the following constant in your wp-config.php:

```
define('CONCATENATE_SCRIPTS', false);
```

### GP-CLI Commands

Enable with:

```
gp site {site.url} -disable-concatenate-load-scripts
```

Disable with:

```
gp site {site.url} -enable-concatenate-load-scripts
```

 

## Block/Unblock Direct PHP Script Execution from wp-content and Subdirectories

Best practice should dictate that all WordPress PHP scripts are called directly by WordPress from within the loop. Assuming best practice is followed you can block PHP execution from all wp-content subdirectories with these CLI commands.

We already block php execution from wp-content/uploads/* so the recent zero day Elementor vulnerabilities would have been mitigated by default, but this command takes things one step further and will also disable direct PHP script execution from the web for any files within any plugin or mu-plugin.

Please be aware, some plugins actually want you to directly call from the web with cronjobs etc. Please ensure if you do so, to use the correct system user for the cronjob to ensure that sites remain isolated by PHP user.

If any plugin you use is allowing direct calling of a PHP script from within a plugin by third party web services – as opposed to using the recommended REST API methods to access WordPress, then the scripts will be being executed by the www-data server user, and will likewise not be isolated.

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/disable-wp-content-php-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/disable-wp-content-php-main-context.conf
```

Which contains configurations to:– Deny access to ../wp-content/*.php

### GP-CLI Commands

Block with:

```
gp site {site.url} -block-wp-content.php
```

Unblock with:

```
gp site {site.url} -unblock-wp-content.php
```

 

## Block/Unblock Comments

WordPress comments can be a nuisance to maintain if your website/s has no need for them. This allows you to easily block them and prevent all the regular spam links for all manner of things that can get you blacklisted in Google. One thing to note with this measure is that it can prevent certain plugins that actually use the WordPress comment system internally. 2 examples of this are:

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/disable-wp-comments-post-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/disable-wp-comments-post-main-context.conf
```

Which contains configurations to:– Deny Access to the wp-comments-post.php

### GP-CLI Commands

Block with:

```
gp site {site.url} -block-wp-comments-post.php
```

Unblock with:

```
gp site {site.url} -unblock-wp-comments-post.php
```

 

## Block/Unblock WordPress OPML Links Functionality

WordPress allows links to be imported or exported using the OPML format via the wp-links-opml.php file. Hitting this page presents an XML output and details of your WordPress installation. Somebad bots will try this page when exploring your site for information. If you are not using this feature, then we may as well disable it at the server level.

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/disable-wp-links-opml-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/disable-wp-links-opml-main-context.conf
```

Which contains configurations to:– Deny Access to the wp-links-opml.php

### GP-CLI Commands

Block with:

```
gp site {site.url} -block-wp-links-opml.php
```

Unblock with:

```
gp site {site.url} -unblock-wp-links-opml.php
```

 

## Block/Unblock wp-trackbacks.php

WordPress has a built-in mechanism to allow trackbacks, notifications on your posts that someone has linked to them. Unfortunately, trackbacks have, in the past, led to several MySQL injection vulnerabilities and if unguarded can lead to a lot of Spam. If you are not using this feature, then we may as well disable it at the server level.

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/disable-wp-trackbacks-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/disable-wp-trackbacks-main-context.conf
```

Which contains configurations to:– Deny Access to the wp-trackback.php

### GP-CLI Commands

Block with:

```
gp site {site.url} -block-wp-trackbacks.php
```

Unblock with:

```
gp site {site.url} -unblock-wp-trackbacks.php
```

 

## Block/Unblock upgrade.php

This WordPress core file is used to manage upgrades of core. It is often used by Bots to identify a site as WordPress, and so this returns a 404 as obfuscation.

Originally we used to make this inaccessible unless deactivated, however, with the many plugins and core updates that require a database upgrade (and the many support tickets that this results in), we have implemented a fix that allows these database upgrades to proceed as long as the request is made directly by the server, but still blocking all other attempts to access the file.

### Nginx

On Nginx this measure now checks the referrer of the request and if it comes from one of its own registered server_name variables, then we know the request has originated from this server and can be processed as a normal PHP request.

### OpenLiteSpeed

OpenLiteSpeed .htaccess can’t check the http_host against the http_referer (which is what Nginx is doing), but we can accomplish the same validation by appending both of these together and then comparing them against a regex.

### Server Configurations

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/block-upgrade-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/block-upgrade-file-main-context.conf
```

Which contains configurations to:– Deny Access to the ../wp-admin/upgrade.php

### GP-CLI Commands

Block with:

```
gp site {site.url} -block-upgrade.php
```

Unblock with:

```
gp site {site.url} -unblock-upgrade.php
```

 

 

### Information - Core and Plugin Updates

If WordPress has upgrade and you can't login, or a plugin requires a database upgrade after updating and it won't complete, be sure to unblock this measure and try again.

## Block/Unblock install.php

This WordPress core file is used to install WordPress, but since we do that for you then is there any need? It is also used by Bots to identify a site as WordPress. If you aren’t needing to install WordPress, then you can disable it at the server level. Sometimes during the management of your server, you might use this file for reinstalling WordPress, depending how you go about things, in such a case please remember to unblock the file.

This CLI command creates the following include on Nginx:

```
/var/www/{site.url}/nginx/block-install-main-context.conf
```

Or here on OLS:

```
/var/www/{site.url}/ols/block-install-main-context.conf
```

Which contains configurations to:– Deny Access to the ../wp-admin/install.php

### GP-CLI Commands

Block with:

```
gp site {site.url} -block-install.php
```

Unblock with:

```
gp site {site.url} -unblock-install.php
```

 

## Disable/Enable Emojis

WordPress emojis can be used to enumerate your WordPress version. They also kinda suck…

### GP-CLI Commands

Disable with:

```
gp site {site.url} -disable-emoji
```

Re-enable with:

```
gp site {site.url} -enable-emoji
```

 

## Disable/Enable RSS

Yet another way to uncover your WordPress version. If you don’t need it, you can disable it.

### GP-CLI Commands

Disable with:

```
gp site {site.url} -disable-rss
```

Re-enable with:

```
gp site {site.url} -enable-rss
```

 

## Disable/Enable Username Enumeration

This blocks all user enumeration attempts on your website. User enumeration is where bots probe your websites for valid usernames so they can attempt to brute force attack you.

For example, the URI “/wp-json/wp/v2/users/” on most WordPress websites openly shows admin names by default. It is well known, and bots will harvest your information from here and other places, then brute force your login page using the valid username/s.

NOTE: The issue with comments returning a 404 error for users who were not logged in has now been resolved in an update to his measure.

### GP-CLI Commands

Disable with:

```
gp site {site.url} -disable-username-enum
```

Re-enable with:

```
gp site {site.url} -enable-username-enum
```

 

## Block/Unblock WP Scan Agent

WPScan is a scanner that attempts to look up all kinds of information about your website, none of which is beneficial to you. It will probe your site for usernames, your WordPress version, themes and plugins you have installed, and a lot more.

A lot of the options throughout this article block all of this, but you can outright block WPScan directly.

### GP-CLI Commands

Block with:

```
gp site {site.url} -block-wpscan-agent
```

Unblock with:

```
gp site {site.url} -unblock-wpscan-agent
```

 

## Block WP Version

This changes your WordPress version to WordPress 42. The change is purely cosmetic and won’t impact your ability to update core/themes/plugins etc, but will prevent bots from being able to access your actual WordPress version and attack you based on known vulnerabilities.

### GP-CLI Commands

Disable with:

```
gp site {site.url} -disable-wp-version
```

Renable with:

```
gp site {site.url} -enable-wp-version
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

