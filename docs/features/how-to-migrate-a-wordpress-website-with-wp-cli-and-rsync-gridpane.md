# How to Migrate a WordPress Website with WP-CLI and rsync | GridPane

# How to Migrate a WordPress Website with WP-CLI and rsync

 

8 min read 

### Table of Contents

 

## Introduction

There are many ways to migrate a WordPress website, but the most efficient is arguably with WP-CLI and a program like rsync.

This is especially true for large websites where plugins often have trouble, and sometimes can’t be used because there’s not enough disk space to create the backup.

This kind of migration is done over the command line and is far more straightforward than most people realize. In this article, we’ll take a look at how to migrate a website to GridPane, but the same steps apply to pretty much any host if you have SSH access and you can modify things accordingly.

In this guide, we’re going to be using the system user for our websites, not the root user.

 

## Part 1. Backup Your Origin Website Database with WP-CLI

You’ll need to connect to your current websites server over SSH to export your backup.

You’ll need to figure out your directory structure and then navigate to your WordPress installation’s directory. As an example, over SSH as the root user on GridPane this is:

```
/var/www/site.url/htdocs
```

Other common paths include:

```
/sites/site.url/htdocs
```

```
/home/systemusername/public_html/
```

```
/home/systemusername/www
```

Once you’re connected to your server you can confirm the correct path.

### Export Your Database

First, make sure you’re running as your website’s system user with:

```
sudo -u systemusername
```

Then use the following command to export your database with WP-CLI:

```
wp db export database.sql --all-tablespaces --add-drop-table
```

It will let you know once the operation is complete and that it was a success. Note that if it’s a big database it can take some time.

 

## Part 2. Create and Prepare Your Destination Website on GridPane

There’s some quick, basic prep work before you begin the migration.

 

### Step 1. Create Your Destination Site

Back in your GridPane account, head over to your Sites page, and create your website. If you have an SSL on your origin site, you may also want to add an SSL.

Leave caching and the security features turned off for now. You can enable them once your site has been successfully imported.

For a guide on creating new websites on GridPane, check out this knowledge base article: New WordPress Website Build Configuration Settings

Once created you have everything you need in place to bring over your origin files, including a newly created WordPress database and properly configured wp-config.php file.

 

### Step 2. Connect to Your GridPane Server

If this is your first time connecting to a GridPane server, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 3. Navigate to Your Sites Directory

Now connected to your server, navigate to your website’s directory with the following command (replacing site.url with your URL):

```
cd /var/www/site.url/
```

 

### Step 4. Remove Your Existing WordPress Files

We’re going to pull over the whole WordPress installation, so first let’s remove the existing one with:

```
rm -R htdocs
```

Now recreate your htdocs directory with:

```
mkdir htdocs
```

GridPane keeps the wp-config.php one level up outside of the /htdocs directory, so we don’t need to worry about making a copy or moving it beforehand.

 

## Part 3. Copy Your Website Files from Your Origin Server to Your GridPane Server with rsync

rsync allows you to both push files from the origin server, or pull files from your destination (GridPane) server. Here we’re going to pull, so the commands below will be ran directly from inside your destination (GridPane) server.

If your server allows you to connect to your server over SSH as the site’s system user and password, the easier route is option 1, where you simply run the command and you’ll be prompted for your SSH password after hitting Enter.

 

### Option 1. Pull your files with rsync: system User + Password

The command below will pull your files from your origin server into your destination. Here’s the basic syntax:

```
rsync -avz -e ssh [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection):/source/* /destination/ --info=progress2
```

Here’s an example you can adjust. You’ll need to switch out the origin server’s IP address, your system user name, the /path/to/site.url, and replace site.url with your website’s URL.

```
rsync -avz -e ssh [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection):/path/to/site.url/htdocs/* /var/www/site.url/htdocs/ --info=progress2
```

You’ll be prompted for your system user’s password, and then the process will begin.

If your origin server is using a custom port (managed hosts like WPEngine, Kinsta, etc, often do), you can specify that with the -p flag as follows:

```
rsync -avz -e 'ssh -p 2222' [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection):/path/to/site.url/htdocs/* /var/www/site.url/htdocs/ --info=progress2
```

 

### Option 2. Pull your files with rsync: System User + SSH Key

Before you begin you need to setup your public and private SSH keys so that your GridPane server can access your origin server. You may wish to use a newly created pair for the migration. Make sure your public key is on your origin server and your private key is on your GridPane server. You may need to check your host’s documentation to get your public key set up correctly on your origin server.

##### Optional: Create a New Key Pair

On your GridPane server you can create a new key pair with:

```
ssh-keygen -t rsa
```

You’ll be ask where you want the files to be created, I recommend:

```
/root/key
```

Now if you list your files with ls -l you’ll see your private key (just named “key”) and public key:

```
root@steves-example-server:~# ls -ltotal 56-rw-r--r-- 1 root root 56 May 23 07:34 2-rw-r--r-- 1 root root 1 May 23 07:50 curr.user-rw-r--r-- 1 root root 6 May 3 07:23 grid.id-rw-r--r-- 1 root root 16 May 3 07:23 grid.source-rw-r--r-- 1 root root 27 May 3 07:31 grid.subdomdrwxr-xr-x 2 root root 4096 May 3 08:00 gridcredsdrwxr-xr-x 2 root root 4096 May 23 07:50 gridenv-rw-r--r-- 1 root root 26 May 3 07:32 gridhttp.auth-rw-r--r-- 1 root root 37 May 3 07:23 gridpane.server.key-rw------- 1 root root 2610 May 23 07:44 key-rw-r--r-- 1 root root 580 May 23 07:44 key.pub-rw-r--r-- 1 root root 3 May 3 07:23 ripley.egg-rw-r--r-- 1 root root 15 May 3 07:31 server.iplrwxrwxrwx 1 root root 26 May 3 07:25 sites-available -> /etc/nginx/sites-availabledrwx------ 4 root root 4096 May 3 07:26 snaplrwxrwxrwx 1 root root 8 May 3 07:25 www -> /var/www
```

Now run the following to display your public key, then highlight it to copy it and you can now add it to your origin server:

```
cat key.pub
```

##### Migrate Your Files

Once your SSH keys are all set, the command below will pull your files from your origin server into your destination (GridPane) server. You’ll need to switch out the key path, system user, IP, website path, and site URL:

```
rsync -avz -e 'ssh -i /path/to/private/key' [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection):/path/to/site.url/htdocs/* /var/www/site.url/htdocs/ --info=progress2
```

If you’ve created a new key pair as above, the path will simply be as follows:

```
rsync -avz -e 'ssh -i key' [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection):/path/to/site.url/htdocs/* /var/www/site.url/htdocs/ --info=progress2
```

If your origin server is using a custom port (managed hosts like WPEngine, Kinsta, etc, often do), you can specify that with the -p flag as follows:

```
rsync -avz -e 'ssh -i /path/to/private/key -p 2222' [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection):/path/to/site.url/htdocs/* /var/www/site.url/htdocs/ --info=progress2
```

Note: Once your migration is complete and you’ve verified everything is working correctly, remove your private key with the following if you’re not migrating any further sites:

```
rm /path/to/private/key
```

 

### Verify Your Files

Once rsync has completed the transfer it will let you know. You can then navigate to your site’s /htdocs directory and verify the transfer has been successful with:

```
cd /var/www/site.url/htdocs
```

And then list your files with:

```
ls -la
```

 

 

### Important

Now that you've migrated your files, check to see if there is a wp-config.php file inside your /htdocs directory. If there is, please rename it before moving on to part 4 below, as this will cause problems with your database import.

## Part 4. Complete Your Migration

Now that you’ve successfully copied your files over, we need to import the database. Please ensure there is not a `wp-config.php` file inside your /htdocs folder before proceeding.
### Import Your Database

If you’re not already in your websites /htdocs directory you can navigate there with the following command (replacing site.url with your URL):
```
cd /var/www/site.url/htdocs
```

It’s generally best to run database imports as your system user instead of using GP-CLI, so run the following command, replacing systemuser with your website’s system user:
```
sudo -u systemuser wp db import database.sql
```

It will let you know once the operation is complete. Note that if it’s a big database it can take some time.
### Run a Permissions Fix

To finish up you can quickly make sure all your file permissions are correctly set with:
```
gp fix perms site.url
```

 

## Part 5. Migration Checks

Regardless of how you migrate your site, you may need to do some clean-up to ensure your website runs smoothly. Below are a few of the most common issues we see.

Once you’ve confirmed your migration has been a success you can enable your caching and security settings.

### Check Database Table Prefix

Depending on where you’re migrating from your database may have a database table prefix that is different from the standard wp_. If this is the case, you will need to update your wp-config.php file.

### Remove Unnecessary Must-Use Plugins

If you’re migrating from a host that uses any must-use plugins, you likely no longer need them and/or need to remove them. You can first disable them by simply renaming the folder.

### Further Checks

If your site still isn’t showing as expected yet, our full diagnosing migrations issue can be found here:

Diagnosing Migration Issues

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

