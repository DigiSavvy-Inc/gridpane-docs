# Additional Security Measure Nginx Includes and Whitelisting | GridPane

# Additional Security Measure Nginx Includes and Whitelisting

 

4 min read 

## Introduction

The GridPane Additional Security measures for WordPress hardening each contain an Nginx include which can be used when are they are active. You can use these includes to customize their behaviour, including adding your own whitelisting.

You can learn more about our Nginx/OLS hardening measures in this knowledge base article:

WordPress Website Hardening for Nginx and OpenLiteSpeed (OLS)

And more about the Security Tab in this article:

Secure Your WordPress Websites: An Overview of the Security Tab

We highly recommend that you check them out.

The includes are for the following settings:

Below details the location of each of these configurations and as you can see below, the includes are at the top of each file.

 

### Disable XMLRPC

Location:

```
/var/www/site.domain/nginx/disable-xmlrpc-main-context.conf
```

Config:

```
include /var/www/site.domain/nginx/*-before-disable-xmlrpc-main-context.conf;fastcgi_hide_header X-Pingback;proxy_hide_header X-Pingback;location = /xmlrpc.php {deny all;}
```

### Disable load scripts concatenation

Location:

```
/var/www/site.domain/nginx/disable-load-scripts-concatenation-main-context.conf
```

Config:

```
include /var/www/site.domain/nginx/*-before-disable-load-scripts-concatenation-main-context.conf;location = /wp-admin/load-scripts.php {deny all;}location = /wp-admin/load-styles.php {deny all;}
```

### Disable wp-content php

Location:

```
/var/www/site.domain/nginx/disable-wp-content-php-main-context.conf
```

Config:

```
include /var/www/site.domain/nginx/*-before-disable-wp-content-php-main-context.conf;location ~* ^/wp-content/.*\.php$ {deny all;}
```

### Disable wp-comments

Location:

```
/var/www/site.domain/nginx/disable-wp-comments-post-main-context.conf
```

Config:

```
include /var/www/site.domain/nginx/*-before-disable-wp-comments-post-main-context.conf;location = /wp-comments-post.php {deny all;}
```

### Disable opml linking

Location:

```
/var/www/site.domain/nginx/disable-wp-links-opml-main-context.conf
```

Config:

```
include /var/www/site.domain/nginx/*-before-disable-wp-links-opml-main-context.conf;location = /wp-links-opml.php {deny all;}
```

### Disable trackbacks

Location:

```
/var/www/site.domain/nginx/disable-wp-trackbacks-main-context.conf
```

Config:

```
include /var/www/site.domain/nginx/*-before-disable-wp-trackbacks-main-context.conf;location = /wp-trackback.php {deny all;}
```

### block install php

```
/var/www/site.domain/nginx/block-install-file-main-context.conf
```

Config:

```
include /var/www/site.domain/nginx/*-before-block-install-file-main-context.conf;location ^~ /wp-admin/install.php {deny all;error_page 403 =404 / ;}block upgrade php/var/www/site.domain/nginx/block-upgrade-file-main-context.confinclude /var/www/site.domain/nginx/*-before-block-upgrade-file-main-context.conf;location ^~ /wp-admin/upgrade.php {deny all;error_page 403 =404 / ;}
```

 

## Quick Reference

At a glance, the above includes are as follows:

```
/var/www/site.domain/nginx/*-before-disable-load-scripts-concatenation-main-context.conf/var/www/site.domain/nginx/*-before-disable-xmlrpc-main-context.conf/var/www/site.domain/nginx/*-before-disable-wp-content-php-main-context.conf/var/www/site.domain/nginx/*-before-disable-wp-comments-post-main-context.conf/var/www/site.domain/nginx/*-before-disable-wp-links-opml-main-context.conf/var/www/site.domain/nginx/*-before-disable-wp-trackbacks-main-context.conf/var/www/site.domain/nginx/*-before-block-install-file-main-context.conf/var/www/site.domain/nginx/*-before-block-upgrade-file-main-context.conf
```

 

## Whitelisting and Modifications for Additional Security Measures

You may at some point have a use case where you want to keep these settings active with the exception of one specific file.

For example, allowing one very specific file to execute PHP while the keeping the Disable wp-content PHP execution measure active for all other PHP files.

Below is an example how you can accomplish this.

 

## Whitelisting the wpDiscuz Plugin

The wpDiscuz plugin executes PHP via:/wp-content/plugins/wpdiscuz/utils/ajax/wpdiscuz-ajax.php

To allow this to work, while still blocking all other PHP files from working we can use the /var/www/site.domain/nginx/*-before-disable-wp-content-php-main-context.conf include inside block wp-content config   /var/www/site.domain/nginx/disable-wp-content-php-main-context.conf.

### Step 1. SSH into your server

Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Create the configuration file

Run the following command to create the configuration file, switching out “site.domain” for your websites domain name:

```
nano /var/www/site.domain/nginx/wpdiscuz-before-disable-wp-content-php-main-context.conf
```

Note: I’ve given the file name the prefix “wpdiscuz” but you change this to make it unique and recognizable for your use case.

### Step 3. Create the location block

Add the following to the file:

```
location ~* ^/wp-content/plugins/wpdiscuz/utils/ajax/wpdiscuz-ajax.php {
   include fastcgi_params;
   set_if_empty $sockfile php;
   fastcgi_pass $sockfile;
}
```

Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

Note: Here we’re using the $sockfile variable, if we change the website’s PHP version this configuration will persist and call the correct PHP .sock file. Learn more about the $sockfile variable here:

PHP Sockfile Variable

### Step 4. Check and Reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

Now PHP execution will still be disabled from /wp-content/plugins directly, but there is an exception for the wDiscuz plugin.

 

## Whitelisting a Directory

Hopefully you will never have to, but if you ever do need to whitelist a specific directory, you can follow the same steps laid out in the wpDiscuz example, only change your location block to look as follows:

```
location ~* ^/wp-content/directory-name-here/.*\.php$ {
include fastcgi_params; 
set_if_empty $sockfile php; 
fastcgi_pass $sockfile; 
}
```

You can swap out directory-name-here for the actual path and directory name you need to whitelist.

Save the file, then check and reload Nginx and you’ll be all set.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

