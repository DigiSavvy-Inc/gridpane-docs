# How to Add Additional System Users to a Website | GridPane

# How to Add Additional System Users to a Website

 

6 min read 

### Table of Contents

 

## Introduction

If you need to give multiple people access to one of your GridPane-hosted websites, and these require separate login details, this isn’t currently possible via your GridPane dashboard. However, you do have a couple of options that you can implement manually over the command line. This article details two avenues available to you.

If this is the first time connecting to your server, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Option 1. Add an additional SSH key to the existing system user

You could add multiple keys to the same system user manually using this file (here {system-user} would be the name of your system user without the brackets):

```
/home/{system-user}/.ssh/authorized_keys
```

That would allow for managing access and rescinding access where needed. You also have the option to connect to your site yourself using an SSH key and giving access to someone else via password, which can then be changed after their work is complete.

However, if you and the third party are both accessing via SSH keys and you’re monitoring the auth.log, this method won’t allow you to distinguish between individuals accessing your site.

 

## Option 2. Create a new system user and grant them access to the website

This second option is more complex. To manually give access to a single directory within Webroot to a different system user and allow for logging, the following steps will walk you through how to do so.

For this, we’ll use an example to demonstrate.

Now I want to give the plugin authors of “awesome-plugin” access to their plugin on the server for a single site, the process would be as follows.

 

 

### Information

Having a separate system user uploading and editing files might lead to permissions issues, so you will be responsible for keeping an eye on that.

## Part 1. Add the New System User

### Step 1. Add a system user for the plugin author on the server

First, head over to the System Users page in your GridPane account and create a new system user.

For example purposes, I am going to call this system user: awesome-plugin-author.

 

### Step 2. Assign Ownership to the Original System User

Connect to the server by SSH and run this command to create a directory in their SFTP home (replacing the system user, site.url, and directory name):

```
mkdir -p /home/{new-system-user}/sites/{site.url}/htdocs/wp-content/plugins/{plugin-directory-name}
```

For example:

```
mkdir -p /home/awesome-plugin-author/sites/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin
```

Next, we also need to assign ownership to the original system user and group:

```
chown -R {orginal-site-owner}:{original-site-owner} /home/{new-system-user}/sites/{site.url}/htdocs/wp-content/plugins/{plugin-directory-name}
```

For example:

```
chown -R king-lazer-cat:king-lazer-cat /home/awesome-plugin-author/sites/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin
```

 

### Step 3. Add the new system user to the site system user group

Run the following, replacing the original system user and new system user as specified:

```
usermod -g {original-site-owner} {new-system-user}
```

For example:

```
usermod -g king-lazer-cat awesome-plugin-author
```

 

### Step 4. Add token files to stop GridPane automated file and directory permissions healing

GridPane has ongoing checks of all WordPress webroot directories and files for 755 and 644 perms, respectively. These two tokens will suspend that function. This also means that for the duration of their existence, you are responsible for maintaining correct permissions.

This is all custom, so if things go awry on a site and it might be permissions, remove these files and wait for a worker to run a heal before creating any support tickets.

Run the following two commands, replacing {site.url} with your sites URL:

```
touch /var/www/{site.url}/disable.automated.dir.perms.healingtouch /var/www/{site.url}/disable.automated.file.perms.healing
```

For example:

```
touch /var/www/lazer-cats.space/disable.automated.dir.perms.healing
touch /var/www/lazer-cats.space/disable.automated.file.perms.healing
```

If you don’t want this healing function, you can also use this file:

```
touch /var/www/{site.url}/custom.perms
```

For example:

```
touch /var/www/lazer-cats.space/custom.perms
```

Into which you could place explicit directory paths and file paths, for example:

```
:/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin/example-file.php::/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin/example-directory:
```

Each line needs delimiting with a starting and ending : colon.

This way, you can control every directory and file you want to maintain custom permissions for, being more restrictive. However, it’s more work, and you are effectively only going to provide access to upload asset by asset.

 

### Step 5. Bind Mount the site plugin directory to the new user directory and persist

```
mount --bind /var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin /home/awesome-plugin-author/sites/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin
```

And add an fstab entry to make sure this persists reboots:

```
echo "/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin /home/awesome-plugin-author/sites/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin none bind 0 0" >>/etc/fstab
```

 

### Step 6. Update plugin and file directories perms to allow system user group write access

```
find "/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin" -not -perm 775 -type d -exec chmod 775 {} \;
find "/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin" -not -perm 664 -type f -exec chmod 664 {} \;
```

You are setting directories to 775 and files to 664.https://chmod-calculator.com/

If in step 4 above you set custom perms on a directory by directory and file by file basis, you should mirror that with setting the group access permissions; the above sets all files and directories in the plugin to give group user write access.

At this point, your new system user awesome-plugin-author should have SFTP access to that plugin directory and its files, they can download and upload files as they need, and their access should be logged separately.

 

 

### Important

When who you're giving access to has completed their work, you should follow the steps below to take things down.

## Part 2. Remove the System User

### Step 1. Reset plugin and file directories perms to remove group write access

Run these commands depending on how you set things up, replacing the example site “lazer-cats.space” with your site URL:

```
rm /var/www/lazer-cats.space/disable.automated.dir.perms.healingrm /var/www/lazer-cats.space/disable.automated.file.perms.healingrm /var/www/lazer-cats.space/custom.perms
```

You can either wait for the worker to run and reset perms to default, or you can then run:

```
find "/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin" -not -perm 755 -type d -exec chmod 755 {} \;find "/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin" -not -perm 664 -type f -exec chmod 644 {} \;
```

 

### Step 2. Remove bind mount and fstab entry

Run the following, replacing the example system user and directory with your own system user and directory

```
umount -lf /home/awesome-plugin-author/sites/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin \&& rmdir /home/awesome-plugin-author/sites/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin
```

Edit the fstab and remove the line you added earlier:

```
nano /etc/fstab
```

Removing this line:

```
/var/www/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin /home/awesome-plugin-author/sites/lazer-cats.space/htdocs/wp-content/plugins/awesome-plugin none bind 0 0
```

Save the file and exit nano with CTRL+O followed by Enter, and then exit with CTRL+X.

 

### Step 3. Delete system user

Now from the GridPane app, you can delete their system user from the System Users page.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

