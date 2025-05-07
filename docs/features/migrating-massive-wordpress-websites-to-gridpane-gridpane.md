# Migrating MASSIVE WordPress Websites to GridPane | GridPane

# Migrating MASSIVE WordPress Websites to GridPane

 

3 min read 

We’ve migrated a lot of websites to our platform over the past few years, as have thousands of users. Some of these were massive websites. We’re talking 50GB websites and WaaS networks with 400+ subsites.

We’ve migrated these types of websites successfully using both the All in One WP Migration plugin and the Migrate Guru plugin.  These two work exceptionally well with the GridPane platform and these are the tools we use more often than not when we run migrations for clients.

Before you get started, however, there are some things you can do to prepare your website and avoid known problems. This article will give you a quick rundown.

## Avoiding Common Problems

You can migrate a small site in a matter of minutes using AIO and Dropbox or Backblaze B2. If small websites fail it’s not really a big deal to simply migrate again a different way. If a massive website fails to migrate it can cost a lot of time and cause a lot of frustration, regardless of whether it fails partway through or makes it all the way over only to not work correctly after the fact.

Fortunately, you can minimize the risk by first checking out issues that are known to cause problems when migrating a website. We have this handy guide that we’ll keep up-to-date as new things come to light. To avoid potential problems from the get-go, highly recommend you check out this article:

Diagnosing Migration Issues

## Preparing your Website

Along with the pointers in the article above, you may also wish to do the following things to prepare your website for the migration:

The above aren’t all strictly necessary (although watch out for Wordfence as it can wreck migration attempts), but it may help your migration go faster and smoother. Number 5 may be overkill for many websites, but the fewer things that can potentially interfere the better.

## Three Tried and Tested Methods

All of the methods below are battle-tested. If you’re going the plugin route then Migrate Guru is 100% free and we’ve been very impressed with it when it comes to migrating mega monster websites.

### 1. Migrate with rsync

This is the preferred method of many experienced developers. It’s by far the quickest and most efficient method if you have the necessary access at your server provider. Here’s our guide on migrating with WP-CLI and rsync:

How to Migrate a WordPress Website with WP-CLI and rsync

### 2. Migrate Guru

We’ve transferred 50GB websites and huge e-commerce and multisite installations successfully with Migrate Guru. It can take its time (30 hours for that 50GB site), but it’s been extremely reliable. Here’s our walkthrough article:

Migrate sites to GridPane using Migrate Guru

### 3. All in One WP Migration

Tried and tested, we’ve migrated huge websites with this plugin, and it’s one of the fastest methods available when using its premium extensions. Check out this article for our walkthrough:

Migrate Sites to GridPane using All In One WP Migration

### 4. Manual Migration

Zipping your site up, exporting its database, and then uploading+unzipping your files, and importing your database is tried and true. Here’s our walkthrough for manually migrating a website:

Manually Migrating a Website to GridPane

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

