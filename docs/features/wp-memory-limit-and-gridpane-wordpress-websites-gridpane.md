# WP_MEMORY_LIMIT and GridPane WordPress Websites | GridPane

# WP_MEMORY_LIMIT and GridPane WordPress Websites

 

6 min read 

## Introduction

Every now again we’re asked a variation of this question on support:

“Why does [insert plugin name] say that the WP_MEMORY_LIMIT is set to 40M?“

The short answer is that the plugin is likely looking at the wp-config.php file and not seeing this explicitly defined, and then returning the default 40M back, instead of assessing the available PHP memory.

For example, WooCommerce and Elementor will return the correct memory limit, whereas Project Huddle will not.

### Table of Contents

 

## Quick Fix

The fix for this is to simply explicitly define the memory limit as follows inside your user-configs.php file, which will automatically insert this into your wp-config.php file when your website is loaded:

```
define('WP_MEMORY_LIMIT', '256M');
```

Or you can set it to always match the PHP Memory Limit (which you can set inside your websites configuration modal) with:

```
define( 'WP_MEMORY_LIMIT', ini_get( 'memory_limit' ) );
```

 

## Editing users-config.php

The user-configs.php file is located in:

```
/var/www/site.url/user-configs.php
```

You can edit it either directly on your server or over SFTP.

### Edit via SFTP

To connect to your server over SFTP, please check out the following articles: –

Connecting to a GridPane Server by SFTP as the Root User

Connecting to a GridPane Server by SFTP as a System User

Once connected, you can download the file over SFTP, make your edits, and then re-upload it to your server.

### Edit via SSH

To connect to your server via SSH, see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

Inside your server, type the following command to edit your user-configs.php, replacing “site.url” with your domain name:

```
nano /var/www/site.url/user-configs.php
```

Make your edits below the following:

```
<?php/*** This file is included in the wp-config.php file.* Users can add their own WordPress configurations here*/
```

Next, save the file with CTRL+O. You can then exit the file with CTRL+X and then exit your server with:

```
exit
```

Once your edits are made, you’re all set! If you migrate your website to a new server or clone it to a new domain name, your custom edits will now persist.

### Learn more about user-configs.php

You can also learn more about the user-configs.php file in the following article, but in a nutshell, to ensure that your wp-config changes persist when you clone a site from one server/domain to another, you should add your customizations here.

Migrations, Cloning, and the wp-config.php File

 

## WordPress and Memory

Before we go any further, let’s take a look at the different memory settings that affect WordPress.

#### 1. PHP Memory Limit

This is the maximum amount of memory your WordPress installation can make use of, set at the server level.

On GridPane, you can adjust the PHP memory limit for your individual websites inside your account by navigating to the Sites page, clicking on your website to open up the configuration modal, and clicking through to the PHP tab.

You can then change the limit here:

All changes made here will then be reflected in your website’s .user.ini file. This is a hidden file located here (replace “site.url” with your domain name):

```
/var/www/site.url/htdocs/.user.ini
```

#### 2. “memory_limit”

When you see memory_limit, this is referring to the PHP Memory Limit as outlined above. I mention this only to avoid any potential confusion should you see it without “PHP” at the beginning.

#### 3. WP_MEMORY_LIMIT

The WP_MEMORY_LIMIT sets the maximum amount of memory that WordPress can use on the front end.

The out-of-the-box default WordPress memory limit is 40M. This means a single PHP script can make use of up to a maximum of 40 MB of RAM.

#### 4. WP_MAX_MEMORY_LIMIT

The WP_MAX_MEMORY_LIMIT sets the maximum amount of memory that WordPress can use in the backend.

 

## GridPane and WordPress Memory Defaults

By default, every new website that you create with GridPane sets the PHP memory_limit to 256MB. The PHP memory limit can easily be changed at any time, as noted in the previous section.

When memory_limit for a site is set at the ini level, it sets the WP_MEMORY_LIMIT internally if it is not set explicitly by use of a constant.

GridPane configures the memory_limit and other PHP settings at a PHP level for the site and its PHP scripts in the .user.ini file as follows:

```
;date.timezone =
default_socket_timeout = 60
session.gc_maxlifetime = 1440
session.cookie_lifetime = 0
short_open_tag = Off
post_max_size = 512M
max_file_uploads = 20
upload_max_filesize = 512M
max_input_time = 60
max_input_vars = 5000
max_execution_time = 300
memory_limit = 256M
```

With this set, the WordPress memory limit is effectively just a wrapper for this ini variable.

WordPress covers this themselves here:

https://wordpress.org/support/article/editing-wp-config-php/

Specifically, they say:

“WordPress will automatically check if PHP has been allocated less memory than the entered value before utilizing this function. For example, if PHP has been allocated 64MB, there is no need to set this value to 64M as WordPress will automatically use all 64MB if need be.”

So once we have defined the memory_limit to 256MB RAM, then WordPress may automatically use this full 256MB no matter whether the WP_MEMORY_LIMIT has been defined explicitly or not.

The reason for this is because in this file in WordPress core: /wp-includes/default-constants.php

You’ll find this code:

 

```
$current_limit = ini_get( 'memory_limit' );
$current_limit_int = wp_convert_hr_to_bytes( $current_limit );
// Define memory limits.
if ( ! defined( 'WP_MEMORY_LIMIT' ) ) {
if ( false === wp_is_ini_value_changeable( 'memory_limit' ) ) {
define( 'WP_MEMORY_LIMIT', $current_limit );
} elseif ( is_multisite() ) {
define( 'WP_MEMORY_LIMIT', '64M' );
} else {
define( 'WP_MEMORY_LIMIT', '40M' );
}
}

if ( ! defined( 'WP_MAX_MEMORY_LIMIT' ) ) {
if ( false === wp_is_ini_value_changeable( 'memory_limit' ) ) {
define( 'WP_MAX_MEMORY_LIMIT', $current_limit );
} elseif ( -1 === $current_limit_int || $current_limit_int > 268435456 /* = 256M */ ) {
define( 'WP_MAX_MEMORY_LIMIT', $current_limit );
} else {
define( 'WP_MAX_MEMORY_LIMIT', '256M' );
}
}
```

 

Here WordPress is checking if the PHP ini value has been set, and if it has it automatically sets that value as the WP_MEMORY_LIMIT internally.

 

## Summary

Some plugins will require WP_MEMORY_LIMIT to be defined.

If a plugin is reporting that your WP_MEMORY_LIMIT is 40M, the quick and easy solution is to explicitly define this inside the user-configs.php file as noted in the Quick Fix section of this article.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

