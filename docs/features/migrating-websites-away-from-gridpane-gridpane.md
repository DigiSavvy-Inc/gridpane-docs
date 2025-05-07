# Migrating Websites Away from GridPane | GridPane

# Migrating Websites Away from GridPane

 

6 min read 

### Table of Contents

 

## Introduction

If you build websites for clients, at some point you will likely need to move a site from GridPane to another host. We understand as agencies you will need to cater to your users, and so we have made efforts to make this as easy as possible when you need to do so.

In this article we’ll look at: –

With full root access and no plugin restrictions, migrating away from us has always been simple, but if you prefer to migrate sites manually it’s now even easier.

 

## Procedure for Migrating via Plugins

To make the migration as smooth as possible you may want to consider the following so that the site doesn’t contain anything unnecessary at the new host: –

The only one above that may actually cause issues at a new host is the SendGrid integration which drops a must-use plugin in with your SendGrid account API details.

If that plugin is still in the site when migrating over you may run into SMTP issues as it can create a conflict with other transactional email solutions.

The others can be removed as they are no longer necessary when migrating and it’s good practice (even if it’s not common practice) to provide your clients with a properly cleaned up website.

 

## Plugin Recommendations

While we don’t support any plugins, you shouldn’t have issues using any popular migration or backup plugins when migrating your website away.

The following are our top choices, in order: –

Your favourite plugin will likely work fine as well if it’s not one of the four above.

 

## GP-CLI Migration Scripts Overview

If you’re a developer and/or prefer to migrate sites via the command line, we have made this incredibly straightforward for you.

 

 

#### Beta Notice

The following GP CLI for migrating away is still in beta. Please proceed with caution if you plan on using it for critical production websites. Any ticket submitted for these GP-CLI commands will be treated primarily as a bug report and there is no critical/urgent support or support guarantees.

The script the GP-CLI is based off can be found on GitHub here:https://github.com/gridpane/outward-bounds/blob/main/outward-bound.sh

However, you can wrap up all websites on a server with just one copy and paste line on the command line to streamline this process for you.

This CLI is still beta, and running it requires you to agree to conditions (detailed in the next section), but it goes a little something like this:

```
gpmigrate-away --dry-run --archive --keep-ini
```

```
gpmigrate-away --dry-run --archive --keep-ini --sites {csv.sites}
```

This takes the wp-config.php, removes all of our settings, and copies it into the htdocs directory. It also removes all our mu-plugins and has a few other options detailed below.

You will still need to export the database, but the installation files will be ready to go.

### GP Migrate Away

gpmigrate-away is the GP-CLI command to prepare and wrap up your websites at the server level, ready for you to migrate to another hosting provider.

### Dry Run

--dry-run is optional and outputs a log of the changes that will happen but doesn’t enact them.

NOTE: Once run in non-dry-run configuration sites will not be properly configured for GridPane services. Subsequently, all sites will be beyond GridPane support responsibility until returned to the previous state.

### Archive

--archive will pack everything up into a tarball (aka a tar archive, which will wrap up all your websites files into one tar file) and move it to a root adjacent directory for SCP/SFTP here:

```
/root/outward-migration-archives
```

### Keep PHP.ini file

--keep-ini will retain the .user.ini in htdocs if you’d like to migrate it.

### Choose Specific Sites or All Sites

--sites accept a single site or a csv list of sites e.g site.com,domain.com,whatever.com etc. Running without specifying a site, or multiple sites will prepare ALL websites on the server. For example:

```
gpmigrate-away --sites example.com,anotherwebsite.com
```

### Help (Manual)

There is also a --help which will open up what we’ve detailed here directly on the command line. Run the following view the details:

```
gpmigrate-away --help
```

 

## Using GP Migrate Away CLI

The following details the process of running our gpmigrate-away CLI. To get started you will need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

In this example, I’ll be packing up all websites on the server, starting with this command:

```
gpmigrate-away --archive --sites example.com,anotherwebsite.com
```

Once ran, it will give the following notice:

 

```
***** THIS IS NOT A DRY RUN *****You are about to run a script to prepare all sites on this server for outward migration.Once run sites will not be GP standard and GP tools will cease to work properly.We take no responsibility for the use of this script, use at your own risk!Do you agree to take responsibility for the use of this script, and would like to proceed (Y/y) or (N/n)?
```

 

Type Y and press Enter to proceed.

Next you’ll see:

```
** You have passed the --archive flag. **Once the script has finished preparing your sites for outward migration,it will then proceed to archive your sites into compressed tarballs here:/root/outward-migration-archivesPlease be aware, you will need to ensure your server has enough free space to accommodate these archives.If your server does not have enough space and this kills your server, that is on you.Do you agree to take responsibility for ensuring you have enough space to create archives, (Y/y) or (N/n)?
```

Type Y and press Enter to proceed.

 

Once the process is complete you will see the following message which details where you can find the archived versions of your websites if you have chosen to archive them:

```
#####################Available Archives:/root/outward-migration-archives/total 62M-rw-r--r-- 1 root root 41M Mar 9 20:40 example.com.gz-rw-r--r-- 1 root root 22M Mar 9 20:40 anotherwebsite.com.gz#####################
```

And you can navigate to them with:

```
cd /root/outward-migration-archives
```

#### All done!

To connect to your server by SFTP, please see the following articles (you will need to connect as the root user to access the /outward-migration-archives folder):

Connect to a GridPane Server by SFTP as Root user

Connect to a GridPane Server by SFTP as System User

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

