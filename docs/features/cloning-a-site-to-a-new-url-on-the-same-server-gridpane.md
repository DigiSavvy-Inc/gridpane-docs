# Cloning a site to a new URL on the same server | GridPane

# Cloning a site to a new URL on the same server

 

8 min read 

### Table of Contents

 

## Introduction

In your workflow, there may be times when you want to clone a duplicate of a site to a new URL, for example:

You can use the GridPane single-site migration/cloning tool located in the site backups to do this. This tool can be used for cloning a duplicate site to the same server or to another destination server.

This article is for cloning a duplicate site to the same server, if you want to clone a duplicate to another server, please see this article instead.

 

 

### Multisite Cloning and Improvements

Same-domain multisite cloning is now fully operational. We've also made improvements to our cloning scripts, and replaced WP-CLI Search Replace with Interconnectit Search Replace, and MySQLDump and import with MyDumper/MyLoader. 
Multisite staging/cloning to a new domain is coming soon!
*Developer plan and above only

## What Settings Clone Across

Cloning a duplicate site with a new URL on the same server will replicate a near-identical state for the site. The duplicate site will belong to the same owner, and it will match all the main control panel settings, including:

We will also duplicate your site-specific PHP in settings and PHP process manager settings that GP-CLI manages, alongside the GP-CLI adjusted site-specific Nginx settings and any includes in your site-level Nginx or OpenLiteSpeed (OLS) directory.

One setting that does not transfer over when cloning is: AutoSSL. This setting is generally only relevant for multisite networks where you want to provision SSL certificates for new Alias domains automatically.

### Cloning to Ubuntu 22.04 Servers

The default system user settings will be applied when you clone websites to Ubuntu 22.04 servers from 18.04 and/or 20.04 servers. This means the system user will have both SFTP and SSH access enabled.

### Getting Started

In this article, we will be using an example development site development.laser-cats.monster to illustrate the steps to migrate this site to a new URL of laser-cats.monster on the same server.

 

## Step 1. Preparation

Before you begin, there may be a few preparation steps you need to take. We also highly recommend that you review the information in this article:

Checks When Migrating/Cloning From One Server to Another

 

 

### Important: Deactivate WP_DEBUG First

If you've had WP_DEBUG active, be sure to deactivate it before you proceed as it may cause a fatal error on the destination site.

### Disk Space

For your clone to begin, our systems require that your server has at least 110% of your site in free disk space. You should ensure you have ample free disk space before you proceed.

### SSL Preparation

An SSL attempt will be made for the newly cloned site IF SSL is enabled on the original site. For this reason, it is important to make sure that your DNS is resolving correctly for the newly cloned site before you attempt cloning. This will speed up the search and replace because the system will just run a single compound regex.

If DNS is not resolving, the clone will proceed as normal, but the SSL attempt will fail. GridPane will then ensure that all URLs in the database for the new site are replaced with HTTP variants, and this requires 3 passes instead of 1. You can then manually enable SSL later.

You can learn more about GridPane search and replace functions here:

GridPane Database Rewrites and Workflow

 

## Step 2. Open the Website Customizer

Click through to your Sites page in the GridPane main menu in your account to go to the Sites management page.

Click on the URL of the site you want to clone a duplicate of in the active site’s panel.

This will open the site customizer.

 

## Step 3. Configure Your URL and Destination Server

Click through to the Clone tab in the site customizer. Here you will find the Migrate/Clone tools.

Here we’ll make use of the second option.

Enter the new URL you’d like to clone your website to, and then select the new server from the dropdown list.

Please remember do not enter the URL with the www host included.

 

### Step 3.1 Clone Information and Staging Site

Click the Migrate/Clone button to open the additional options modal:

At the top you’ll see the URL and destination server information, as well as a checkbox for whether to include the staging site. Here, a staging site doesn’t exist so the option is greyed out. However, if you do have a staging site you can clone this as well – check the box if you’d like to do so.

 

### Step 3.2 Database Rewrite Options

Below the information you’ll be presented with tabs to configure your new website, the first being whether to “Include Database Rewrites“.

Generally, you’re going to want to run database rewrites. This will run a search and replace and ensure that all of your URLs are set correctly. Two options are available to you:

InterconnectIT is usually the best option as it’s more comprehensive. WP-CLI might be a little quicker, but it also has a higher chance of missing some rewrites.

 

### Step 3.3 Set Your System User

In the next tab you can choose whether to use the same system user or create a new one. All the regular options are available:

We always recommend that every site have their own individual system user.

 

### Step 3.4 Set SMTP

If you would like to set your SMTP API key you can choose this here:

 

### Step 3.5 DNS Settings

If you would like to configure a DNS API provider for the site you can choose from your available keys:

 

### Step 3.6 Set Your Local Backups

You can configure your local backups on the new site to match the current site settings, leave them turned off, or set an entirely custom schedule:

If setting different settings you have full granular controls just like in the backups tab:

 

### Step 3.7 Set Your Remote Backups and Start Your Clone/Migration

Like local backups, you can choose to match the sites current settings, leave remote backups turned off, or set a new custom schedule:

Full configuration options are available for one chosen provider:

Once set you’re now ready to begin your migration.

 

### Step 3.8 Clone Your Website

Once configured, click the Migrate / Clone Now button.

Please be patient while the duplicate cloning process is ongoing, and refrain from making any changes to your site and server.

You will receive a string of notifications to keep you informed about how the migration/clone is proceeding throughout the process. Please pay attention to these.

When the process is complete, your new site will appear in the active sites list.

Your settings on your newly cloned website will match up with your origin site.

 

## Step 4. Check Your Cloned Website

You should check your duplicate site to make sure everything is as expected. The content and database will have been cloned across, and the URLs and file paths will have been updated to the new URL.

We will have matched most states for the GridPane features, including all PHP ini settings, PHP process manager settings, and Nginx configuration settings that have been adjusted by GP-CLI. We will also have migrated across cloned files from your Nginx includes directory.

Please ensure that everything has cloned correctly before deleting your previous site, and consider keeping the original for 1-2 weeks while backups on the new site have time to take place.

 

 

### Note

Should a site clone fail to complete for any reason, it will leave a copy of the gzip file in place that looks like GPBUP-2.website.com-CLONE.gz. We have had one report of this being left behind after a successful clone. This is very uncommon, but should you find the process has not deleted this gzip file after successfully cloning your website, you can delete this manually.

## Cloning Staging Websites

As noted in Step 3.1, you can choose to clone your staging site along with the main site if you would like to do so.

You can also clone individual staging sites to a different URL either on the same server or a new server if you have a need to do so though. You will find the same options for cloning in your staging site’s customizer, and you can follow the same steps above like you would when cloning a production website.

One thing you can’t do, however, is create or clone staging sites to “staging” subdomains on GridPane. For example, if you try to create the website “staging.website.com” as a regular site, it will fail and result in an error message. This will also fail in the exact same way during the cloning process.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

