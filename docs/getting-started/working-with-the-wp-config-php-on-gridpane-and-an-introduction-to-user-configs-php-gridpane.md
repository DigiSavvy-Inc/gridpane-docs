# Working with the wp-config.php on GridPane and an introduction to user-configs.php | GridPane

# Working with the wp-config.php on GridPane and an introduction to user-configs.php

 

5 min read 

## Introduction

If you have a website that requires you to add custom code snippets to the wp-config.php file, on GridPane these changes won’t persist when you migrate your website to a new server or clone it to a new domain name. Due to the way cloning works, a new wp-config.php will instead be generated in its place.

To remedy this, we have the user-configs.php which you can use to add your custom edits. We’ll dig into all the details in this article.

 

## Working with wp-config.php on GridPane

In a nutshell, please don’t edit the wp-config.php file for your websites unless absolutely necessary (for example, changing the database table prefix, updating a database user, or editing the DB_CHARSET),

Don’t manually edit the custom edits that we take care of from our side -these  all have a comment beginning with GridPane, for example: /* GridPane Cron */.

If you need to add additional information to the wp-config.php we have a special include that you can use called user-configs.php that you can use instead.

### Migrating to GridPane and wp-config.php

If you migrate to GridPane and the migration process copies the wp-config.php file into your websites /htdocs folder, this may cause issues, and you will need to delete the none-GridPane wp-config.php file to ensure your site works as expected.

We’ll take a look at both of these below.

 

## A Quick Intro to user-configs.php

user-configs.php is a custom GridPane solution for adding content to wp-config.php without actually adding it directly to the wp-config.php file.

Code placed in this file is treated in the same way by WordPress as if it was added to the wp-config.php file. This is accomplished using the PHP include statement.

With this, you can make sure that your changes do persist over migrations/clones, by instead adding your code to the user-configs.php file. Any code added here will not be written over at any point by any GridPane function.

NOTE: This wouldn’t transfer over if moving a WordPress site away from GridPane, but it will make it so moving and cloning sites within GP is smooth sailing.

 

## Editing users-config.php

The user-configs.php file is located in:

```
/var/www/site.url/user-configs.php
```

You can edit it either directly on your server, or over SFTP.

### Edit via SFTP

To connect to your server over SFTP, please check out the following articles: –

Connecting to a GridPane Server by SFTP as the Root User

Connecting to a GridPane Server by SFTP as a System User

Once connected you can download the file over SFTP, make your edits, and then re-upload it to your server.

### Edit via SSH

To connect to your server via SSH, see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

Inside your server type the following command to edit your user-configs.php, replacing “site.url” with your domain name:

```
nano /var/www/site.url/user-configs.php
```

Make your edits below the following:

```
<?php/*** This file is included in the wp-config.php file.* Users can add their own WordPress configurations here*/
```

Next, save the file with CTRL+O. You can then exit the file with CTRL+X, and then exit your server with:

```
exit
```

Once your edits are made you’re all set! If you migrate your website to a new server, or clone it to a new domain name, your custom edits will now persist.

 

## Migrating to GridPane and the wp-config.php file

To ensure your migrations are successful, please double check that you don’t have two wp-config.php files inside your site as you move your sites to GridPane

GridPane securely stores the wp-config.php file 1 level up outside of /htdocs here:

```
/var/www/site.url
```

Depending on how you’ve migrated over, you find that you also have additional file here:

```
/var/www/site.url/htdocs
```

If you have two wp-config.php files these can interfere with each other and cause problems. Please simply delete the wp-config.php file inside /htdocs if it exists, and leave ours in it’s place.

You can do this by connecting to your server over SFTP or you can delete them directly on your server – please see the guides linked in the previous section to get started.

If deleting over SSH, you can navigate to your websites htdocs folder with the following command (switching out “site.url” for your websites domain name):

```
cd /var/www/site.url/htdocs
```

Then display the contents of the file with:

```
ls -l
```

And if you see a wp-config.php file, you can delete it with:

```
rm wp-config.php
```

Once that’s done you’re all set!

 

## Cloning, Failover, and wp-config.php

Cloning and Failover largely follow the same functions.

When moving a site from one server to another, your user-configs.php will be cloned over, copying any customizations that you’ve made.

The table prefix inside the wp-config.php will also be matched on the new site.

Important: When using Snapshot Failover, if you later edit the table prefix on the primary server for any reason, this will not be copied a second time, so please be sure to edit this on both the primary site and the failover site.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

