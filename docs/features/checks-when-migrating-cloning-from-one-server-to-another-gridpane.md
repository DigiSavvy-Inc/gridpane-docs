# Checks When Migrating/Cloning From One Server to Another | GridPane

# Checks When Migrating/Cloning From One Server to Another

 

4 min read 

## Introduction

There will come a time when you need to move your websites from one server to another. This may be to give a specific site more resources, such as moving a growing WooCommerce store to its own individual server or upgrading from an older version of Ubuntu to a newer version.

Whatever the reason, this article outlines some of the checks that you may want to include in your own internal processes.

### Table of Contents

Special thanks to Pascal Brennecke for outlining the basis of this article over in our Facebook group.

 

## Confirm Your Clone/Migration Was Successful

Just like when migrating a site from another host to GridPane, you should always confirm that your migration was successful.

GridPane’s cloning system is extremely reliable, but even with our systems, it is still your responsibility as the website owner/host to ensure all went well.

Just like regular migrations, if you have errors in your codebase, it’s possible that these could affect our processes.

### Confirming Without Changing DNS

The easiest way to check over your sites before you update the live DNS is to use a local host redirect. This will instruct your device to ignore the live DNS records and instead connect to the IP address that you specify. To get started, check out this article:

How can I edit my local hosts file to redirect URLs

 

## GridPane Server and/or Site Settings

### Server-wide Configs or Custom Work

If you’ve set up any server-level configs, such as an Nginx config for using WP Rocket for Nginx or enabling webp, then you’ll also need to make sure these are set up once again on the new server.

Unlike site-specific configurations, these will not be cloned across when moving sites from one server to another.

If you’ve added anything custom, such as installing additional software, or server level cronjobs, then you will also need to manually move/install/recreate these on your new server if they are still needed.

### Site Specific Settings

Any custom Nginx or OLS configurations that have been added to:

```
/var/www/site.url/nginx/var/www/site.url/ols/var/www/site.url/user-configs.php
```

Will all be cloned across when using our cloning features. Other site-specific settings will too. For full details on what will and won’t clone, please be sure to read the applicable cloning article as there are differences:

 

## Update Your DNS Records

Once you’ve confirmed that your website has been cloned/migrated successfully, you can now change your DNS records.

Or, if you’re using a floating IP address, you can flip this over from the old server to the new server.

In most cases, this will take a few minutes to go live worldwide. Especially if you’re using a service like Cloudflare or DNS Made Easy (DNSME).

### Flushing DNS Records

“DNS Propagation” is the time it takes to publish or update DNS records. However, what actually takes time and causes the “24-48” hour delays you often see notices about, is the clearing of the previously cached version of these records across the internet.

Fortunately, it’s possible to speed this up by manually clearing out these records. This article has all the details:

Speeding Up DNS Propagation: Manually Clearing Out Cached Records

### CDNs and IP addresses

If you’re using a CDN with your website, make sure that any settings associated with the IP are in sync with the new server IP address.

 

## When to Change DNS on a Busy Website

When migrating a busy, dynamic website, planning a scheduled window where you put the website into maintenance mode on the live server and migrate the site will likely be necessary.

This will prevent important database data from being lost, such as e-commerce orders, membership sign-ups, LMS course progress, etc.

The above steps still apply – once you’ve migrated the website, you’ll want to thoroughly check your site over before changing the DNS.

Once you’ve confirmed the migration was a success, you can then update the DNS and bring the site out of maintenance mode.

 

## IP Addresses and Website Email

While an IP address’s “status” doesn’t matter for your website’s SEO (or so all indicators seem to point to), they can make a difference in your email deliverability.

This only applies if mail is being sent directly from your server’s IP vs using an API-driven service such as SendGrid that sends from its own IP addresses. If this is something that concerns you, you can check your server IP status here:

https://mxtoolbox.com/blacklists.aspx

Generally though, this is not something that you need to worry about.

### Email Auth, SPF, etc

If you have set up an Auth service, such as Google Workspace or Gmail to send email, you may need to add this new IP address to your allow/whitelist. For example, this is Google’s procedure:

Add IP addresses to allowlists in Gmail

You’ll also want to make sure you update SPF records for email verification, if applicable.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

