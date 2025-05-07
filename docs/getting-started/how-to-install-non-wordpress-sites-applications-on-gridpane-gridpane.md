# How to Install Non-WordPress Sites/Applications on GridPane | GridPane

# How to Install Non-WordPress Sites/Applications on GridPane

 

3 min read 

 

### Warning

Please do not install non-WordPress applications on servers that contain your WordPress websites as this may void the warranty of that server and interfere with our ability to serve you effectively on support. Please be sure to read this article before you proceed: 
Can I install other Applications on a GridPane managed server?

### Table of Contents

 

## Introduction

We’ve debated on whether to create this article or not for some time. Technically we’re built for WordPress, and while you can run other PHP-based applications (and they will probably perform pretty damn well), it’s not something we can ever provide direct support for.

Please heed the warning box above and install your site/application directly on its own server.

Below is a quick basic rundown of the process.

 

## Step 1. Install a WordPress Site

The easiest way to install a non-WordPress site on GridPane is to first create the site as a WordPress site using our app and then provision an SSL certificate. This will create all configurations on the server that will serve files from this site’s directory.

Please see the following article and SSL archive to get started:

 

 

### A note on SSL certificates

In our testing these have been provisioned without any issues even when after removing WordPress from htdocs, but that testing was also very limited.

## Step 2. Remove the WordPress Files

Next, remove all of the WordPress files from your htdocs directory.

To remove the WordPress files, you will first need to SSH into your server. Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

Now navigate to your website’s directory with the following command (replacing “yourwebsite.com” with your own domain name):

```
cd /var/www/yourwebsite.com
```

Next, remove the htdocs directory with the following:

```
rm -R htdocs
```

​This will remove all WordPress files leaving you with a clean slate to install your application.

Now we just need to recreate the htdocs folder with:

```
mkdir htdocs
```

 

## Step 3. Upload your site/application

Depending on how you’re transferring your site/application, you can pretty much take it from here if you’re downloading via wget.

If you’re uploading over SFTP, please see the following guides to get started:

 

## Step 4. Import your database (if applicable)

If your site has a database you should be able to import that directly into the database that was created for your WordPress site through PHPMyAdmin:

Connect to your GridPane Site Database with PHPMyAdmin

NOTE: The database user that we create doesn’t have permission to create databases, but you should have no issues dropping the tables in the database we create and uploading your own.

 

 

### Database Credentials

Your database credentials are safely stored outside of the htdocs directory inside /var/www/yourwebsite.com/wp-config.php. In step 2 when we deleted htdocs, we did not delete the wp-config.php file. If you need them, you can find your database credentials here.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

