# How to Fix the “Cookies are blocked or not supported by your browser” Error | GridPane

# How to Fix the “Cookies are blocked or not supported by your browser” Error

 

2 min read 

The following error sometimes presents itself when trying to login to the subsite of a WordPress multisite:

“ERROR: Cookies are blocked or not supported by your browser. You must enable cookies to use WordPress.”

This may occur even if your browser does in fact have cookies enabled and it can happen when WordPress is serving all of your multisites cookies from one domain, instead of each individual domain.

The fix is usually simple. Below is how to solve it.

 

 

### IMPORTANT

If you're using a custom login URL, then it's highly likely that the login page is being cached, and this is the root cause of the issue. Please see the following article on how to exclude a page from Nginx caching:
Exclude a page from server caching

## Step 1. Connect to Your Server

You can connect to your server via SFTP or SSH. In this example, we’ll be looking at connecting to the server by SSH. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Edit the “user-configs.php” File

We’re going to place our code inside the user-configs.php file. You can learn more about this file here:

Migrations, Cloning, and the WordPress Configuration File (wp-config.php)

The contents of this file is inserted directly into the wp-config.php file using a PHP include statement. Any code added here will not be written over at any point by any GridPane function, and it will persist over migrations/clones.

### Edit the file

Open the user-configs.php file for editing with the following command (replacing “site.url” with your websites domain name):

```
nano /var/www/site.url/user-configs.php
```

Add the following to the file:

```
define('ADMIN_COOKIE_PATH', '/');
 define('COOKIE_DOMAIN', '');
 define('COOKIEPATH', '');
 define('SITECOOKIEPATH', '');
```

Now save the file with CTRL+O followed by Enter. Close the file with CTRL+X.

 

## Step 3. Check Your Website

At this point, you’re all set! All that’s left is to test your website again in an incognito window to confirm you can now log in.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

