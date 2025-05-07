# How to Backup / Export / Import a WordPress Database | GridPane

# How to Backup / Export / Import a WordPress Database

 

4 min read 

## Introduction

There are multiple, quick, and easy ways to backup your website’s database. In this article, we’ll look at two different options: phpMyAdmin and WP-CLI.

### Table of Contents

There are also popular plugins you could use, such as All in One WP Migration, UpdraftPlus, WP Database Backup WP Migrate DB, and BackWPup.

 

## Exporting via phpMyAdmin

If your database is small, phpMyAdmin should work perfectly well for exporting and importing your database. It’s quick, and you can do it right inside your GridPane account.

In your account, open up phpMyAdmin by clicking the database icon next to your website.

Inside phpMyAdmin, click “Databases” at the top of the page.

In the left-hand sidebar, you can see the databases available. Select your website’s database (in this example, the website is “waas.monster”.

Once inside your database, scroll down to the bottom and check the “Check all” box, and then select the export option from the dropdown to the right of the check box.

phpMyAdmin will take you to a new page as shown below. Click “Go” and it will automatically start the download of your database.

 

## Importing via phpMyAdmin

Now we need to import the database. Open up phpMyAdmin like in the step above. In the menu at the top, click on “Import“.

Click the “Choose file” button and add your database, then scroll to the bottom of the page and click “Go“.

This may take a while depending on the size of your database, but you’ll see a success screen once complete.

 

## Exporting via WP CLI

### Step 1. Connect to Your Server

For this you’ll need to connect to your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Backup Your Database

Creating a backup of your database with GP-WP-CLI is quick and easy.

Run the following command to backup your database (switching out “site.url” for your domain name:

```
gp wp site.url db export /var/www/site.url/htdocs/name_of_backup.sql --all-tablespaces --add-drop-table
```

For example:

```
gp wp gridpane.com db export /var/www/gridpane.com/htdocs/dbaug2020.sql --all-tablespaces --add-drop-table
```

NOTE 1: Full path to the .sql file should be entered even if the command is being run from the directory (say htdocs) where the SQL file is present.

NOTE 2: If the above gives you a permissions error, your website may require you to add additional privileges. This will look something like this:

```
mysqldump: Error: Access denied; you need (at least one of) the SUPER or SET_USER_ID privilege(s) for this operation
```

Please see this guide for reference on how to grant extra privileges:

How to grant SUPER permissions for your website

 

## Importing via WP CLI

If your database backup isn’t already on your server, you can upload via SFTP into your htdocs folder.

Next, navigate there with:

```
cd /var/www/site.url/htdocs
```

Now in the folder where our database is located, we can run the following GP-WP-CLI command to import it:

```
gp wp site.url db import /path/to/database.sql
```

For example:

```
gp wp example.com db import /var/www/example.com/htdocs/database.sql
```

 

 

### NOTE

The full path to the .sql file should be entered even if the command is being run from the directory (say htdocs) in which the sql file is present.

### If you get an error when trying to import..

While still inside your websites /htdocs folder, try running WP CLI directly instead of GP-CLI.

First, try the following, replacing “systemuser” with your websites system user:

```
sudo -u systemuser wp db import database.sql
```

Alternatively, you can swap over to your websites system user with the following (make sure you use your website’s actual system user):

```
su mywebsiteuser
```

And from here you can run your WP-CLI commands without our GP wrapper. On the command line, it will then look a little different from running as the root user – here’s an example:

```
root@myserver:/var/www/example.com/htdocs# su mywebsiteusermywebsiteuser@myserver:/var/www/example.com/htdocs$
```

The command from here is as follows:

```
wp db import database.sql
```

You can return back to running as the root user with:

```
exit
```

More information on using WP-CLI on GridPane servers can be found in this article:

How to Use GP WP-CLI and Regular WP-CLI on GridPane Servers

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

