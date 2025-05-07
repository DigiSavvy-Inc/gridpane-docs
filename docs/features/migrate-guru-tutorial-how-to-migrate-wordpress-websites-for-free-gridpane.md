# Migrate Guru Tutorial: How to Migrate WordPress Websites for Free | GridPane

# Migrate Guru Tutorial: How to Migrate WordPress Websites for Free

 

9 min read 

### Table of Contents

 

## Introduction

Of all of the plugins that are available to migrate a WordPress website from one host to another, Migrate Guru is one of the most reliable and one of the easiest to use.

Tens of thousands of websites have been migrated from other hosts to GridPane, including 70GB news websites, 450+ subsite multisites, and pretty much every kind of website you can imagine. For big websites it can take some time (sometimes 24+ hours for truly huge websites), but it is incredibly reliable and 100% free.

We highly recommend it, and once you’ve migrated your first website, any future websites will be quick and easy.

### Origin and Destination Note

In this article, we will be referring to the site you wish to migrate as the origin site and the site or server being migrated into as your destination site or server.

 

 

### Multisite Notice

1. If you're migrating in a multisite, be sure to toggle on the appropriate multisite setting in your website customizer BEFORE you begin. Learn more here:
How to Enable WordPress Multisite on GridPane

2. Be sure to set the correct URL when migrating a multisite. DONT use a temporary URL/domain as you will not be able to change this after the migration has completed. Instead, use a local hosts redirect to check your migration has been successful:

How can I edit my local hosts file to redirect URLs

## Migration Options: Migrate Guru Key vs SFTP Credentials

There are two migration methods available with Migrate Guru. The original method was to enter the SFTP details of the destination site.

The newer, easier method uses a key/token – a unique identifier that is used to authenticate and authorize the migration process between two websites – that you can get by installing Migrate Guru on your destination site, copying a migration key from the settings there, and then entering that inside Migrate Guru on your origin site.

This article will cover both options.

 

## Migrating Multiple Sites? Create a Bundle

If you’re migrating multiple websites, why not create a bundle inside your GridPane account that installs and activates the Migrate Guru plugin for you?

This will eliminate the need to install the plugin manually each time, and save you a little bit of time per website.

Learn how to create a bundle here: Using GridPane Bundles.

 

## Step 1. Set Up Your Destination Website

You’ll need a server and your destination website set up and created before you begin. If you don’t already have these set up, these articles offer some getting started guidance:

### Provision an SSL Certificate

If possible, it’s always best to provision an SSL certificate before you begin your migration.

If you’re using Cloudflare or DNSME, you can provision an SSL before you change your DNS records by using the DNS API domain verification method. Alternatively, if the website’s DNS is not using either Cloudflare or DNSME, you can use the proxy challenge method instead. Details can be found in these articles:

### Migrate Guru Key

If using the token option to migrate your website, log in to your destination website, install and activate the Migrate Guru plugin, and then click through the plugin settings page. Here you will see the the option to create a migration key:

Click this and it will reveal your key:

Click the clipboard icon to copy it.

 

## Step 2. Configure Your Origin Website

Now that your destination website is set up, it’s time to configure the Migrate Guru plugin inside of your origin website.

If you haven’t already, go ahead and install and activate Migrate Guru on your origin site.

Go to Migrate guru and add your email address and then agree to the terms & conditions to proceed.

On the next page, select “Other Host”:

The name of this may vary in the future, so if that’s the case, you’re looking for the option that isn’t a specific host.

 

## Step 2.1 Key Method Configuration

Once you have your key from your destination website, the key method is super simple. On the migration configuration page, simply enter your key:

That’s it! Now just click the Migrate button to begin your migration.

 

## Step 2.2 SFTP Method Configuration

By default, Migrate Guru will show you the key migration option. To change to SFTP, click “Manually Input Host Details“:

From here, carefully add the SFTP details of your destination site. Here is filled out example:

### Destination Site URL

On the Destination URL, if the site has SSL then it’s https://

Without SSL it’s http://

### FTP Type

Select SFTP.

### Destination Server IP and Port

Add your destination server on GridPane. You can ignore the port.

### FTP Username

Add the System User you created for the destination site.

### FTP Password

You can find your password on the System Users page. Find your system user and click on the little eye icon to open up and view your password:

Alternatively, you can create a new password by clicking on the padlock icon:

### Directory path on Ubuntu 20.04

On Ubuntu 20.04, the directory path looks as follows: /sites/site.url/htdocs

For example:/sites/example.com/htdocs

### Directory path on Ubuntu 22.04

On Ubuntu 22.04 (including PeakFreq servers), the directory path looks as follows:/home/system-user-name/sites/site.url/htdocs

For example:/home/mysiteuser/sites/mywebsite.com/htdocs

 

## Step 3. Start Your Migration

Once all your information has been added, click the Migrate button at the bottom of the page to begin your migration. If all the details are correct then you should get this page below.

Once the migration has completed, you should get a confirmation message and email.

 

## Step 4. Test Your Site on GridPane

Make sure you test the migrated site on GridPane. Check both the front end and the dashboard if all was migrated.

Use your local host to redirect URL. This is how to go about it.

Once you have confirmed the migration was successful you can safely flip DNS to the GridPane Server.

 

 

### Important

Please double check that another wp-config.php has not been transferred over inside your websites /htdocs folder.

## Troubleshooting

Your migration may have gone flawlessly, but there may be an issue or two that may need correcting once complete.

The common one we see is directly below – if you or you’re host have configured a custom database table prefix, then you may need to update this in your wp-config.php file.

 

### Incorrect Database Table Prefix

###### The Problem

You’ve imported your site, but all the plugins are deactivated and content is missing.

###### Diagnosis

We sometimes see this when migrating from managed hosts such as Kinsta and WP Engine. Here you need to check to see if the database table prefix is “wp_”. You can do this by clicking on the database icon next to your website to open up phpMyAdmin:

We’re looking to see if these match up (be sure to check thoroughly as the original database tables from the sites creation may still be there):

A custom prefix could potentially be anything, but often looks something like: “wp87f_“

###### The Solution

If your table prefix doesn’t match up, but all your database tables are using the same prefix, you can edit the table prefix in your wp-config.php via SFTP (download, edit, reupload) or the command line.

To edit via the command line type the following command (switch out “site.url” with your domain name):

```
nano /var/www/site.url/wp-config.php
```

Edit your prefix, and then hit Control+O, and then enter to save the file. Exit with Control+X.

 

### Checking for and deleting duplicate wp-config.php files

To ensure your migration has been successful, you may also want to double check that you don’t have two wp-config.php files inside your site. If you have one inside /htdocs you should delete or rename it.

```
/var/www/site.url/htdocs
```

GridPane securely stores the wp-config.php file 1 level up outside of /htdocs here:

```
/var/www/site.url
```

If you have two wp-config.php files these can interfere with each other and cause problems. Please simply delete the wp-config.php file inside /htdocs if it exists, and leave ours in it’s place.

You can do this by connecting to your server over SFTP:

Connect to a GridPane Server by SFTP as Root user

Or you can delete them directly on your server – please see the following guides to get started setting up your SSH Keys, and connecting over SSH:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

Once connected to your server, you can navigate to your websites htdocs folder with the following command (switching out “site.url” for your websites domain name):

```
cd /var/www/site.url/htdocs
```

Then display the contents of the file with:

```
ls -l
```

And if you see a wp-config.php file, you can rename it with:

```
mv wp-config.php wp-config.php_old
```

This will ensure that WordPress no longer uses it in anyway. If you have any info you need in this file, you can copy it and then add it to your websites user-configs.php file.

Once you no longer need it, you can remove it with:

```
rm wp-config.php
```

Once that’s done you’re all set!

 

### Must-Use Plugins Causing Errors

###### The Problem

A common issue we see is that plugins installed by the previous host result in critical errors, sometimes breaking the site entirely. Sometimes they can make a site extremely slow, or result in other PHP errors.

This is a very common practice nowadays. If migrating a site from GridPane to another platform, you will also want to remove our must-use plugins first as well.

###### Diagnosis

Normally, these are installed as Must-Use plugins, and they can be found inside:

```
/var/www/site.url/htdocs/wp-content/mu-plugins
```

(The above is the GridPane directory structure). This can be accessed by SSH or SFTP.

A quick way to test if this will fix your website is to rename this folder temporarily and retest your site.

###### Solution

If the issues you were seeing on your website are now resolved, you can leave this folder in its renamed state for the moment so that you have all the plugins for reference. Once you know what you need and what you don’t, you can remove the ones you don’t need entirely.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

