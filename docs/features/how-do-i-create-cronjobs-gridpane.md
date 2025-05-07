# How do I create cronjobs? | GridPane

# How do I create cronjobs?

 

4 min read 

One of the most useful tools on your NGINX server is Cron. Backups, updates, SSl renewals, they’re all run using the cron service. And it’s not just for sysadmin jobs, you can customize it to include any job you want and run it on any schedule you want.

### Video Intro and Walkthrough

Big thank you to Augus van Gils from the GridPane community for putting this great video walkthrough together. If you’re new to creating your own cronjobs or need a refresher, this video will help you get started.

 

 

First, you’ll want to generate an SSH key, and login as root to your server.  If this is your first time doing this, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

You can also run the following command to switch user into your system user and add user-level cronjobs:

```
su systemusername
```

By default, sites are added as gridpane, but you can create a custom system user and assign the sites to it. It’s ideal to create a unique custom system user for each site.

Here’s a great resource for figuring out what time you want things to run:

https://crontab.guru/

 

## Cron.d Cronjobs

Cronjobs in the crontab that are created by GridPane have a self-healing mechanism should something occur where they are wiped out.

However, this self-healing doesn’t apply to custom jobs, and while this is a rare occurrence, we have seen a couple of separate reports of this exact issue. This is something you should be aware of and requires your consideration.

Information on creating/editing cronjobs via the crontab is outlined in the sections below, but you may wish to consider adding your custom cronjobs into /etc/cron.d.

### About cron.d

Originally cron.d wasn’t created for the purpose explained in this article. Its original goal was to allow Linux packages to create cronjobs without needing to modify the crontab directly. However, you can also make use of cron.d to ensure that your custom cronjobs persist

It’s important to note that these are run as the root user, and this must be specified (details in the example below).

You can learn more about /cron.d over at the Debian manpage here.

### Naming Format

The naming format here is important. Your cronjob names must “consist solely of upper- and lower-case letters, digits, underscores, and hyphens. This means that they cannot contain any dots.”

### Example

Here’s an example of a cronjob added via /cron.d. Create the cronjob with:

```
nano /etc/cron.d/your-cronjob-name
```

Add your job in the regular format as outlined in this document, but with the username (root) after the timing settings. For example, this:

```
* * * * * /usr/local/bin/gp wp example.com something
```

Would be as follows instead:

```
* * * * * root /usr/local/bin/gp wp example.com something
```

CTRL+O and then Enter to save the file. CTRL+X to exit nano.

 

## Viewing and Creating/Editing Crontab Cronjobs

To view existing cronjobs, you can view them with:

```
crontab -l
```

You can edit and add your own jobs with:

```
crontab -e
```

Here you’ll need to select an editor. We recommend “nano”.

 

## System User Specific Cronjobs

You can also run the following command to switch user into your system user and add user-level cronjobs:

```
su systemusername
```

By default, we encourage individual system users for individual websites when you create new sites inside your GridPane account.

You can also create a custom system user and assign the sites to it. It’s ideal to create a unique custom system user for each site.

 

## Timing Cronjobs

Here’s a great resource for figuring out what time you want things to run:

https://crontab.guru/

If you’re not already familiar with creating cronjobs (or even if you are), we can definitely recommend Crontab Guru as an excellent resource.

 

## Example Cronjobs

The following are a couple of example cronjobs. Some also make use of GP WP-CLI, which you can learn more about here:

GP WP-CLI

### 1. Clearing the cache for a specific SITE

Clear the cache for a specific site once every 12 hours (or to be more specific, at minute 0 past every 12th hour):

```
0 */12 * * * /usr/local/bin/gp fix cache example.com
```

### 2. Flushing Permalinks

Flush permalinks for a specific website every 30 minutes via GP-CLI:

```
30 * * * * /usr/local/bin/gp wp example.com rewrite flush
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

