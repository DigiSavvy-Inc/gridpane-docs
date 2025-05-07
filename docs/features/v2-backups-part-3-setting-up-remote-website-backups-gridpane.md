# V2 Backups Part 3. Setting Up Remote Website Backups | GridPane

# V2 Backups Part 3. Setting Up Remote Website Backups

 

5 min read 

### Table of Contents

 

## Introduction

GridPane’s remote backup system allows you to back your websites up at four different external providers. We recommend three types of backups for your security and ability to recover from worst case scenario type situations: –

A backup or several on your local machine isn’t a bad idea either. We highly recommend you take advantage of the remote backup options available to you. Storage at each of these providers is relatively inexpensive – especially Backblaze and Wasabi.

 

## Setup Your API Credentials

You can choose from four different providers – Backblaze, Wasabi, Amazon S3, and Dropbox. To get started, below are links that will help you create and then set your API keys inside your GridPane account: –

 

## Getting Started with Remote Backups

To get started, head over to the Sites page in your account:

Then click on the name of any of your websites to open up the site configuration modal, and navigate through to the backups tab.

Here you’ll see the new options available for the new backup system. You’ll see both local and remote options are located in this tab, and you can learn more about local backups in this article:

Local Website Backups

 

 

### IMPORTANT

You must select your backup provider as shown in the section below if you want to activate automatic backups. We regularly get support tickets that remote backups cannot be activated, but this is always due to no backup provider being specified.

## Set Your Backup Provider/s

Before you can setup your remote backups you need to have API keys added to your account. If you haven’t done this yet, please choose a provider and follow the articles linked above to get your API keys created and added to GridPane.

Once you have API keys configured, you will be able to select your provider from the “Select Remote Storage Provider” dropdown.

Choose your provider, choose the specific API key you wish to use, and click the “Add Remote Storage” button.

This will immediately create a remote backup of your website.

Once this has finished you will be able to set up automatic backups and take manual backups, and the restore and purge options for your remote storage option will then become available.

 

## Automatic Backups

You have the option to set your remote backups on an automatic schedule. This can be set at any of the following intervals:

Select your preferred schedule from the dropdown, then choose the specific time you would like backups for this website to take place.

Once you’ve configured your choices, hit the Update button to confirm.  If you’re unsure about what time to choose, simply select the start of the hour.

Backups will then take place automatically according to this schedule.

 

## Manual Backups

You can remotely backup your websites manually any time you need to do so.

You can also tag your backup to make it easily identifiable if you later need to use it to restore your website.

 

## Restoring Backups

You have the ability to restore your remote backups to the same server your production site is hosted on, or to a site with the same URL on a different server. The following two sections will walk you through the process.

 

 

### Information: Restoring Very Large Websites

When restoring a remote backup, the files will be downloaded before it is restored, and it will not overwrite files in real time. Please ensure that you have ample disk space available for the process to run - as a general rule of thumb, you should have at least 2.5 times the size of the site in free disk space before running your restore.

## Restoring from a Remote Backup

If you ever need to restore one of your websites from a remote backup you can do so quickly and easily. Below the remote backup options you’ll find the Restore options.

Select remote from the first dropdown, then choose either automatic or manual from the second, and then choose the backup you wish to restore from in the third dropdown.

When you’ve selected your backup hit the “Restore Now” button.

If you’re not seeing the backup you’re looking for, hit the “Refresh” button to get ensure all of the latest backups are available for you to view.

 

## Restoring on a Different Server

If you’re restoring a backup of your website to a different server, the steps below make this quick and simple.

### Step 1. Create a site with the same domain

To restore a remote backup from a different server, first create a site with the same domain (if you want to change the name after you can do this easily by either cloning the site or using the primary domain change function).

### Step 2. Fetch all potential sources

Open your sites customizer and click through to the Backups tab.

Here you will see a big blue button labeled “Fetch All Potential Sources“. This will search for all remote backups for this site that have been created for same URL but on other servers – which includes existing servers and/or previous servers.

Click the button to run a search for other servers that host the same domain.

### Step 3. Select Your Server and Provider

Now you can select the server and specific backup provider you want to restore from.

Click the “See What’s Available” button.

If you need to, you can also refresh the available sources by clicking the Refresh Sources button.

### Step 4. Select and Restore

Now select your desired backup and hit the restore.

 

## Further Reading

For further information about how backup systems work, the available options for configuring them, and for setting up remote backups (available on V2), please see the articles listed below.

### Strategy

Recommended Backup Strategy

### V2 Backup Documentation

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

