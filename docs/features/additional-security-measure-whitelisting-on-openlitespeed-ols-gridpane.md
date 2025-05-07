# Additional Security Measure Whitelisting on OpenLiteSpeed (OLS) | GridPane

# Additional Security Measure Whitelisting on OpenLiteSpeed (OLS)

 

2 min read 

## Introduction

While OpenLiteSpeed comes with a .htaccess file that supports Apache mod_rewrite rules, we recommend that you add your custom rewrite rules to the auto-generated rewrites.conf file located in:

```
/var/www/site.url/ols/rewrites.conf
```

Your custom rewrite rules take place before any of the GridPane core rewrite rules are appended, and with this you can create whitelists for the additional security measures.

In particular, you can whitelist certain plugin files for the Block /wp-content PHP measure which prevents PHP from executing outside of the WordPress loop.

 

## Whitelisting

You may at some point have a use case where you want to keep these settings active with the exception of one specific file.

For example, allowing one very specific file to execute PHP while the keeping the Disable wp-content PHP execution measure active for all other PHP files.

Below is an example how you can add whitelist rules for any of the additional security measures.

 

## Whitelisting the wpDiscuz Plugin

The wpDiscuz plugin executes PHP via:/wp-content/plugins/wpdiscuz/utils/ajax/wpdiscuz-ajax.php

To allow this to work, while still blocking all other PHP files from working we can use the rewrites.conf to add our rewrite rule.

### STEP 1. SSH INTO YOUR SERVER

Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Add your Rewrite Rule

Edit the rewrites.conf with the following command (replace “site.url” with your domain name):

```
nano /var/www/site.url/ols/rewrites.conf
```

And add the following:

```
RewriteCond %{REQUEST_URI} ^/wp-content/plugins/wpdiscuz/utils/ajax/wpdiscuz-ajax.php$ [NC]RewriteRule .* - [L]
```

Now hit Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

### Step 3. Rebuild your vhconf

As the rewrites.conf file has been modified, a specific OpenLiteSpeed command has to be executed in order for the changes to take effect (replace “site.url” with your domain name):

```
gpols site site.url
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

