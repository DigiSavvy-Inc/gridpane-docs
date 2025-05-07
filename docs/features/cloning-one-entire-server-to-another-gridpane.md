# Cloning One Entire Server to Another | GridPane

# Cloning One Entire Server to Another

 

3 min read 

## Introduction

GridPane makes moving your websites from one server to another a simple process. This article will walk you through the available configuration options and offers some tips for before and after you start the cloning process.

### Table of Contents

 

 

### Canary Sites

Canary sites are skipped during the cloning process and so are not transferred from your origin server over to your destination server.

## Preparation: Before You Begin

Before you begin, there may be a few preparation steps you need to take. We also highly recommend that you review the information in this article:

Checks When Migrating/Cloning From One Server to Another

 

 

### Important: Deactivate WP_DEBUG First

If you've had WP_DEBUG active on any of your websites, be sure to deactivate it before you proceed as it may cause a fatal error on the destination site.

### Server-Wide Configs or Custom Work

If you’ve set up any server-level configs, such as an Nginx config for using WP Rocket for Nginx or enabling webp, then you’ll also need to ensure these are set up once again on the new server.

Unlike site-specific configurations, these will not be cloned across when moving sites from one server to another.

If you’ve added anything custom, such as installing additional software or server-level cronjobs, then you will also need to manually move/install/recreate these on your new server if they are still needed.

### Disk Space

Ensure that your destination server has ample disk space. This means that should you have at least double enough for all your sites, with space left over.

 

## Configure Your Server Clone

To get started, head over to the Tools page in your GridPane account and then select the Server Clone in the Tools.

Select your Origin server and your Destination server, and choose if you want to clone only production websites or both production sites and their staging sites:

Next, if you would like to match the local and/or remote backup configurations, check the boxes:

When you’re ready, click Start Task, and your server clone will begin.

 

 

### Important: Before You Delete Your Origin Server...

Once the process completes, check that your sites are working as expected and flip DNS to the new server. As a recommendation, we would suggest keeping your old servers for two weeks to ensure that everything is good before decommissioning them.

## The Cloning Process

The server cloning process follows the same procedure as cloning a site with the same URL from one server to another. You can read our full article here:

Cloning a duplicate site with the same URL to a different server

Specifically, it will copy all production websites across, including the following settings:

We will also duplicate your site-specific PHP in settings and PHP process manager settings that GP-CLI manages, alongside the GP-CLI adjusted site-specific Nginx settings and any includes in your site-level Nginx or OpenLiteSpeed (OLS) directory.

One setting that does not transfer over when cloning is: AutoSSL. This setting is generally only relevant for multisite networks where you want to provision SSL certificates for new Alias domains automatically.

### Cloning to Ubuntu 22.04 Servers

The default system user settings will be applied when you clone websites to Ubuntu 22.04 servers from 18.04 and/or 20.04 servers. This means the system user will have both SFTP and SSH access enabled.

 

 

### Multisite Cloning and Improvements

Same-domain multisite cloning is now fully operational. We've also made improvements to our cloning scripts, and replaced WP-CLI Search Replace with Interconnectit Search Replace, and MySQLDump and import with MyDumper/MyLoader. 
Multisite staging/cloning to a new domain is coming soon!
*Developer plan and above only

## Safety First

Please ensure that all of your sites have cloned correctly before deleting your origin server, and consider keeping all of the original sites for 1-2 weeks while backups have time to take place.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

