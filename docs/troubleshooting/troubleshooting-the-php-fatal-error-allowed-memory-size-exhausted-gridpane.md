# Troubleshooting the “PHP Fatal error: Allowed memory size exhausted” | GridPane

# Troubleshooting the “PHP Fatal error: Allowed memory size exhausted”

 

5 min read 

## Introduction

The “allowed memory size exhausted” fatal PHP error means that a PHP script exceeded the set PHP memory limit and thus failed. This can result in 500 errors or broken functionality within a webpage.

The error will be available either in your website Nginx or OpenLiteSpeed error log and will look like this:

```
PHP Fatal error: Allowed memory size of 134217728 bytes exhausted (tried to allocate 10485760 bytes) in {script-path-here} on line 370
```

Fortunately, this is a quick and easy fix, and below we’ll cover the two scenarios that you may encounter.

### Table of Contents

 

## Understanding the PHP Memory Limit

PHP.net breaks PHP memory_limit down like this:

This sets the maximum amount of memory in bytes that a script is allowed to allocate. This helps prevent poorly written scripts for eating up all available memory on a server. Note that to have no memory limit, set this directive to -1.

This setting is per-script, which means that other scripts on the same page may execute like normal (since they have their own memory allocation), and only a portion of the page will be broken. In other cases, it could cause a 500 HTTP error, and the page may fail to load altogether.

More often than not, when we see this error, it’s usually due to a WordPress plugin.

### How Much Should You Increase It?

Increase the memory enough to resolve the error from happening, and then simply leave it there. If it requires more than 512MB, then this is potentially problematic and you should address the issue directly within your code base (usually, it’s finding a replacement for a plugin).

Setting a high memory limit does not provide any additional benefit and can actually result in issues that are otherwise easy to avoid. By setting a high memory limit you’re allowing the possibility for poorly written code to consume all of your RAM and potentially cause performance issues across ALL of the sites on this server, and you would also be oblivious to any future code issues that may arise.

 

## 1. Website PHP Memory Limit Exhausted

GridPane sets a default size of 256MB, which is plenty for almost all use cases, even WooCommerce. This is fairly standard for the industry.

It is generally better to find and fix the code responsible for needing more memory, but you can also easily increase the PHP memory limit inside your website customizer > PHP INI settings.

To get started, navigate to the Sites page inside your account and click on the name of the website to open up the customizer. Here, you’ll find the memory setting located inside PHP > PHP INI here:

Enter the new memory limit and hit update.

### Alternative Option: Set via GP-CLI

Alternatively, you can set this via GP-CLI with the following command:

```
gp stack php -site-mem-limit {integer} {site.url}
```

For example:

```
gp stack php -site-mem-limit 512 gridpane.com
```

 

## 2. PHP CLI Memory Limit Exhausted

It’s far rarer to encounter this error, but it’s possible you could run into it using WP-CLI on the command line.

### Step 1. Check php.ini used

Connect to your server via SSH and run the following:

```
wp --info
```

### Step 2.1 Nginx

On Nginx, the output will look as follows, and we’re specifically looking for the highlighted line:

```
OS: Linux 4.15.0-197-generic #208-Ubuntu SMP Tue Nov 1 17:23:37 UTC 2022 x86_64
Shell: /bin/bash
PHP binary: /usr/bin/php8.0
PHP version: 8.0.25
php.ini used: /etc/php/8.0/cli/php.ini
MySQL binary: /usr/bin/mysql
MySQL version: mysql Ver 8.0.30-22 for Linux on x86_64 (Percona Server (GPL), Release '22', Revision '7e301439b65')
SQL modes:
WP-CLI root dir: phar://wp-cli.phar/vendor/wp-cli/wp-cli
WP-CLI vendor dir: phar://wp-cli.phar/vendor
WP_CLI phar path: /root
WP-CLI packages dir: /root/.wp-cli/packages/
WP-CLI cache dir: /root/.wp-cli/cache
WP-CLI global config:
WP-CLI project config:
WP-CLI version: 2.7.1
```

The current CLI PHP version across GridPane servers is 8.0 as above. We can increase the memory_limit by editing this file with:

```
nano /etc/php/8.0/cli/php.ini
```

### Step 2.2 OpenLiteSpeed

On OpenLiteSpeed, the output will look as follows, and we’re specifically looking for the highlighted line:

```
OS: Linux 5.4.0-122-generic #138-Ubuntu SMP Wed Jun 22 15:00:31 UTC 2022 x86_64
Shell: /bin/bash
PHP binary: /usr/local/lsws/lsphp80/bin/php
PHP version: 8.0.26
php.ini used: /usr/local/lsws/lsphp80/etc/php/8.0/litespeed/php.ini
MySQL binary: /usr/bin/mysql
MySQL version: mysql Ver 8.0.30-22 for Linux on x86_64 (Percona Server (GPL), Release '22', Revision '7e301439b65')
SQL modes:
WP-CLI root dir: phar://wp-cli.phar/vendor/wp-cli/wp-cli
WP-CLI vendor dir: phar://wp-cli.phar/vendor
WP_CLI phar path: /root
WP-CLI packages dir: /root/.wp-cli/packages/
WP-CLI cache dir: /root/.wp-cli/cache
WP-CLI global config:
WP-CLI project config:
WP-CLI version: 2.7.1
```

The current CLI PHP version across GridPane servers is 8.0 as above. We can increase the memory_limit by editing this file with:

```
nano /usr/local/lsws/lsphp80/etc/php/8.0/litespeed/php.ini
```

### Step 3. Adjust and Save

Use the down arrow key to scroll down to “Resource Limits“, and you’ll find the setting under:

```
; Maximum amount of memory a script may consume
; http://php.net/memory-limit
memory_limit = XXX
```

Edit the limit value (numbers only), then save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

### Step 4. Restart PHP

Finally, restart the appropriate PHP version with:

###### 4.1  NGINX

```
gp php {php.version} -restart
```

For example:

```
gp php 8.0 -restart
```

###### 4.2 OPENLITESPEED

```
touch /usr/local/lsws/admin/tmp/.lsphp_restart.txtsystemctl restart lsws
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

