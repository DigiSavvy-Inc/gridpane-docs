# Cloning a site with the same URL to a different server | GridPane

# Cloning a site with the same URL to a different server

 

6 min read 

### Table of Contents

 

## Introduction

There may be times when you need to clone a site from one server to another. GridPane makes this process simple, and you can use the GridPane single site migration/cloning tool located in the site configuration mode > backups tab.

This article is for cloning a duplicate site with the same URL to a different server, but you can also: –

 

 

### Multisite Cloning and Improvements

Same-domain multisite cloning is now fully operational. We've also made improvements to our cloning scripts, and replaced WP-CLI Search Replace with Interconnectit Search Replace, and MySQLDump and import with MyDumper/MyLoader. 
Multisite staging/cloning to a new domain is coming soon!
*Developer plan and above only

## What Settings Clone Across

Our cloning tool will replicate a near-identical state for the cloned site. The duplicate site will belong to the same owner if that user exists on the server, and it will match all the main control panel settings, including:

We will also duplicate your site-specific PHP in settings and PHP process manager settings that GP-CLI manages, alongside the GP-CLI adjusted site-specific Nginx settings and any includes in your site-level Nginx or OpenLiteSpeed (OLS) directory.

One setting that does not transfer over when cloning is: AutoSSL. This setting is generally only relevant for multisite networks where you want to provision SSL certificates for new Alias domains automatically.

### Cloning to Ubuntu 22.04 Servers

The default system user settings will be applied when you clone websites to Ubuntu 22.04 servers from 18.04 and/or 20.04 servers. This means the system user will have both SFTP and SSH access enabled.

 

## Step 1. Preparation

Before you begin, there may be a few preparation steps you need to take. We also highly recommend that you review the information in this article:

Checks When Migrating/Cloning From One Server to Another

 

 

### Important: Deactivate WP_DEBUG First

If you've had WP_DEBUG active, be sure to deactivate it before you proceed as it may cause a fatal error on the destination site.

### Server-Wide Configs or Custom Work

If you’ve set up any server-level configs, such as an Nginx config for using WP Rocket for Nginx or enabling webp, then you’ll also need to make sure these are set up once again on the new server.

Unlike site-specific configurations, these will not be cloned across when moving sites from one server to another.

If you’ve added anything custom, such as installing additional software or server-level cronjobs, then you will also need to manually move/install/recreate these on your new server if they are still needed.

### Disk Space

For your clone to begin, our systems require that your destination server has at least 110% of the origin site in free disk space, but you ensure you have ample free disk space before you proceed.

 

## Step 2. Open Your Website Customizer

Click on the Sites link in the GridPane main menu to go to the Sites management page.

Click on the URL of the site you want to clone a duplicate of in the active site’s panel.

This will open the site customizer.

 

## Step 3. Configure the Destination Server

Click through to the Clone tab in the site customizer. Here you will find the Migrate/Clone tools:

Here, we’ll make use of the first option.

Simply select the new server from the dropdown list as pictured below:

 

### Step 3.1 Clone Information and Staging Site

Next, click the Migrate / Clone Now button. This will open up a new window that looks as follows:

At the top you’ll see the URL and destination server information, as well as a checkbox for whether to include the staging site. Here, a staging site doesn’t exist so the option is greyed out. However, if you do have a staging site you can clone this as well – check the box if you’d like to do so.

 

### Step 3.2 System User Options

Below the information you’ll be presented with tabs to configure your new website, the first being setting your system user.

Here you can choose whether to use the same system user or create a new one. All the regular options are available:

 

### Step 3.3 Set Your Local Backups

You can configure your local backups on the new site to match the current site settings, leave them turned off, or set an entirely custom schedule:

If setting different settings you have full granular controls just like in the backups tab:

 

### Step 3.4 Set Your Remote Backups and Start Your Clone/Migration

Like local backups, you can choose to match the sites current settings, leave remote backups turned off, or set a new custom schedule:

Full configuration options are available for one chosen provider:

Once set you’re now ready to begin your migration.

 

### Step 3.5 Start Your

Please be patient while the duplicate cloning process is ongoing and refrain from making any changes to your site and either the origin server or the destination server.

You will receive a string of notifications to keep you informed about how the migration/clone is proceeding throughout the process. Please pay attention to these.

When the process is complete, your new site will appear in the active sites list.

Your settings on your newly cloned website will match up with your origin site.

 

## Step 4. Check Your Cloned Website

You should check your duplicate site to make sure everything is as expected. The content and database will have been cloned across, and the URLs and file paths will have been updated to the new URL.

We will have matched most states for the GridPane features, including all PHP ini settings, PHP process manager settings, and Nginx configuration settings that have been adjusted by GP-CLI. We will also have migrated across cloned files from your Nginx includes directory.

Please ensure that everything has cloned correctly before deleting your previous site, and consider keeping the original for 1-2 weeks while backups have time to take place.

 

 

### Note

Should a site clone fail to complete for any reason, it will leave a copy of the gzip file in place that looks like GPBUP-2.website.com-CLONE.gz. We have had one report of this being left behind after a successful clone. This is very uncommon, but should you find the process has not deleted this gzip file after successfully cloning your website, you can delete this manually.

## Cloning and Staging Websites

As noted in Step 3.1, you can choose to clone your staging site along with the main site if you would like to do so.

You can’t create or clone staging sites to staging subdomains on GridPane. For example, if you try to create the website “staging.website.com” as a regular site, it will fail and result in an error message. This will also fail during the cloning process.

You can clone it to a different URL either on the same server or a new server if you have a need to do so though. You will find the same options in your staging site’s customizer.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

