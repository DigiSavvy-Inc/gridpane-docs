# Manually Migrating a Website to GridPane | GridPane

# Manually Migrating a Website to GridPane

 

12 min read 

## Introduction

If you’re having difficulty migrating your website using a plugin, then a manual migration can be a quick and reliable way to migrate a website to GridPane.

This is the long-winded, manually download and then upload over SFTP method. It’s far less efficient than using rsync or scp, but it will get the job done if you’re new to the command line.

You will need FTP/SFTP access at your current host for the method outlined in this article to work, and this will work for both regular WordPress sites and WordPress multisites. In this article, I’ll be manually migrating a small WP Ultimo website.

### Table of Contents

 

## Part 1. Exporting Your Database

If your database is small, PHPMyAdmin should work perfectly well for exporting and importing your database. If you have a large database, however, exporting via the command line will be necessary.

### Exporting via PHPMyAdmin

Head over to PHPMyAdmin in your current hosting account and log in. If you’re using cPanel or Plesk, simply clicking on the icon in your account should log you right in.

If you’re using a managed hosting server, the login details are usually available inside your account in your website’s specific page. If you can’t find them, a quick Google search for “host-name PHPMyAdmin login” should provide the info you need on locating these details.

Once logged in, click “Databases” at the top of the page.

In the left-hand sidebar you can see the databases available. Select your website’s database (in this example the website is “waas.monster”.

Once inside your database, scroll down to the bottom and check the “Check all” box, and then select the export option from the dropdown to the right of the check box.

PHPMyAdmin will take you to a new page as shown below. Click “Go” and it will automatically start the download of your database.

You can move on to part 2.

### Exporting via WP-CLI

If your host supports it, this is quicker and easier than exporting via MySQL.

Navigate to your /htdocs folder and run the following command:

```
wp db export database.sql --all-tablespaces --add-drop-table
```

### Exporting via MySQL on the Command Line

For this, you’ll need to open up your wp-config.php file and then connect to your server.

Your wp-config file contains the database username, database name, and database password. We’ll need all three to run our export.

Inside your server, navigate to your /htdocs folder (so we can export the database with the rest of the files and import via WP CLI later on) and run the following command, switching out “USER_NAME” and “DATABASE_NAME” for your actual details:

```
mysqldump --opt -u USER_NAME -p DATABASE_NAME > database.sql
```

Example:

```
mysqldump --opt -u waas_monster -p waas_monster > database.sql
```

You’ll be prompted for your password, copy and paste in your password from your wp-config here.

Your server will create the file “database.sql”.

 

## Part 2. Export Your Website Files from Your Current Host

To migrate, we’ll need to copy all of the files in our WordPress installation, and your database if you exported this via the command line.

This includes your themes, plugins, uploads (images, etc), and any other files which have been added to your /wp-content directory. If you’ve used a backup plugin before you may want to check to see if you have any backups stored here and remove any that aren’t necessary to reduce the size of your download.

If your website is relatively small and simple, you’re probably fine just copying the /wp-content folder, but it’s a safer bet to transfer ALL files and it’s not much (if any) extra work.

The contents of your WordPress folder will look like this, and we’ll be copying the entire directory over:

Also, check to see if the wp-config.php file is located outside of the main folder where your website is stored – here at GridPane we store it outside of htdocs for security and other hosts may too – more on this in part 4.

### Migrating from cPanel or Plesk

If you’re migrating from cPanel or Plesk, you can export your website quite easily inside your account via the file manager.

Here you can zip all of your WordPress files (see image above), and download them all in just one zip file.

If you’re unsure of how to do this, check out the following articles:

You can now skip to part 3.

### Migrating Without a File Manager

If you have direct access to your servers, you can create a zip file containing all your websites folders/files via the command line – many managed hosts provide direct server access.

To get started, SSH into your server (see your hosting provider’s instructions) and navigate (cd) to your website’s directory. For example, my htdocs folder is the directory I want to zip (for you it may be “public_html”), and for me, this is located in “/var/www/waas.monster” so I’ll run:

```
cd /var/www/waas.monster
```

Confirm the folder containing your directory by running to view all the files and directories:

```
ls -l
```

My htdocs is indeed here, so now I’m going to zip the directory with the following command:

```
zip -r mychosenfilename htdocs
```

Example

```
zip -r waasmonterbackup htdocs
```

The above command names zips up everything inside htdocs into a file called waasmonsterbackup.zip (name your zip file whatever makes sense for you).

### Download Your Website Files via SFTP

Unfortunately, Filezilla and other FTP clients don’t support compression (to my knowledge), so if you’re using Filezilla or another FTP client and don’t have access to your server to zip everything up, you will need to download them all as is. This may take some time.

Log into your website via SFTP – you’ll need to get the correct details from the current host and either download all of the files inside your website’s folder or the zip file you created.

If you’ve created a zip file, just drag and drop this into your computer.

If you don’t have a zip file, create a folder on your computer to store your website’s files in, and then select all of the files and drag and drop them from your FTP client into your folder.

Once your download has finished, select all of your files except your wp-config.php file and move these into a folder named “htdocs”. If you exported your database via the command line, include this here too.

Next right-click on your new htdocs folder and “Send to” > “Compressed (zipped) folder“.

We’ll now be able unzip htdocs in exactly the right place in part 4.

 

## Part 3. Create a New WordPress Website in GridPane

Create your new WordPress website inside your GridPane account as you would normally do for creating any website and continue to step 4.

NOTE: As I’m importing a subdomain multisite, I’m going to go ahead and toggle on the subdomain multisite option inside the site configuration modal here at this stage too. This of course would apply if you’re moving a multisite as well.

 

 

### Multisite Notice

If you're migrating in a multisite, be sure to toggle on the appropriate multisite setting in your website customizer BEFORE you begin. Learn more here:
How to Enable WordPress Multisite on GridPane

## Part 4. Upload Your Website Files

Now we need to upload our website’s files to the server. Before we can do that, however, we need to remove the WordPress files that are already there. Deleting these via SFTP is certainly possible, but it’s unnecessarily long-winded, and as we’ll be using the command line anyway, let’s delete these directly on our server.

To do this we’re going to:

We’ll then upload our zipped website file into the main website directory via SFTP, and unzip it via the command line.

### Step 1. SSH into Your GridPane Server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Prepping Your Website via the Command Line

To remove the files from your brand new WordPress installation, run the following command and switch out “site.url” for your domain:

```
rm -r /var/www/site.url/htdocs
```

Example:

```
rm -r /var/www/waas.monster/htdocs
```

### Step 3. Upload Your Zipped Website (and Database if Applicable) Over SFTP

To connect to your GridPane server over SFTP, please see these two articles. You can connect as root or as a system user – whichever option is easier for you:

Connect to a GridPane Server by SFTP as Root user

Connect to a GridPane Server by SFTP as System User

Once connected, navigate through to your website’s main directory: (root/var/www/yourdomain.com). Here is where you can upload your website.zip file from part 1. You can also upload your database from part 2 at this time as well.

To begin your upload, select your file/s and then drag and drop it into your htdocs folder in your FTP client.

### Step 4. Unzip Your Website Files

Back inside your server, we can now unzip your file. Please note that your website needs to live inside a folder called “htdocs”, so if the file you are unzipping isn’t contained in that folder, you can create it with the following and then upload your zip file there:

```
mkdir /var/www/site.url/htdocs
```

Upload your files. In my case, I named my zipped website file “waasmonsterbackup.zip”. First, navigate to your website’s main folder:

```
cd /var/www/site.url
```

Or htdocs if appropriate:

```
cd /var/www/site.url/htdocs
```

Then unzip the file as follows:

```
unzip yourfilename.zip
```

Example:

```
unzip waasmonsterbackup.zip
```

### Step 5. Add Any wp-config.php Customizations (if Applicable)

If your old wp-config has any customizations that were specific to your website then you can add these into your website’s user-configs.php file, which is a GridPane-specific include. You can learn more about this file in this article:

Working with the wp-config.php on GridPane and an introduction to user-configs.php

If there’s nothing there that isn’t already inside the GP version, you can skip this part.

The user-configs.php file is located in:

```
/var/www/site.url/user-configs.php
```

You can edit it either directly on your server, or over SFTP. To edit on your server you can run the following (replacing site.url with your website URL):

```
nano /var/www/site.url/user-configs.php
```

Once you’ve made your customizations you can save the file with CTRL+O followed by Enter. Then exit nano with CTRL+X.

 

 

### Important

One final thing: You’ll need to be sure that you haven’t uploaded your previous wp-config file into htdocs as having two exist together (one inside htdocs, one outside) will cause problems/totally break your website.

## Part 5. Import Your Database

If your database is less than 512mb in size, you can use PHPMyAdmin to upload it.

If it’s larger, this will require uploading via SFTP and importing via the command line.

### Importing via PHPMyAdmin

Open up PHPMyAdmin by clicking the database icon next to your website.

Click through to your database as you did in step 2, and then scroll to the bottom and check the “Check all” box. Before we import our database, we need to drop all of the existing tables for this new installation.

Open the dropdown to the right of the checkbox and select “drop“.

You’ll be asked: “Do you really want to execute the following query?”

Select “Yes” (as this is a brand new WordPress installation there’s no risk here – just make sure you’ve opened the right database!).

Now we need to import the database. In the menu at the top, click on “Import“.

Click the “Choose file” button and add your database, then scroll to the bottom of the page and click “Go“.

### Importing via WP-CLI

As we’ve uploaded our database into our website’s /htdocs folder, first run this command to navigate there:

```
cd /var/www/site.url/htdocs
```

Now in the folder where our database is located, we can run the following GP-WP-CLI command to import it:

```
gp wp site.url db import database.sql
```

### Importing via MySQL on the Command Line

This is here primarily for reference purposes, the WP CLI commands above are easier and simpler.

Navigate to your websites:

```
cd /var/www/waas.monster/
```

Now we’re in the folder where our database is located we can run the following command to import it:

```
mysql -u USER_NAME -p DATABASE_NAME < database.sql
```

We’ll need to switch out “USER_NAME” and “DATABASE_NAME” again. To find these details, open up your website’s configuration modal and click the “Display wp-config” button as shown below:

NOTE: If your database table prefix is not “wp_”, then you will need to edit this in your wp-config.php file.

 

## Part 6. Finishing Up

Now that your website has been imported, head over to the Tools page inside your GridPane account. Use the self-help tools to first reset the permissions, and then run a full cache clear.

At this point, you may need to provision an SSL certificate before you view your website. To do this without changing your DNS, please see our API integration articles:

Once these have been completed it’s time to check out your website and thoroughly check it over just like you would with any website you migrate from one place to another.

WP Ultimo Note: As I’m moving a WP Ultimo site, I’m going to finish by running our Ultimo commands on this site, and then clear the cache.

### ZIP FILE AND DATABASE CLEAN UP

Back on your server you can also remove your zip and database files from your website directory. To do this, first navigate there with:

```
cd /var/www/site.url
```

And then run:

```
rm yourfilename.zip
```

And if you uploaded your database here too, run:

```
rm database.sql
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

