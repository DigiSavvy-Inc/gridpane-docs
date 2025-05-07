# How to Migrate to GridPane with Zero Downtime | GridPane

# How to Migrate to GridPane with Zero Downtime

 

4 min read 

## Introduction

Whether this is possible is a common question that we get asked, and you can absolutely migrate your websites to GridPane and experience zero downtime.

The contents of this article will guide you from server creation to successful website migration, and also help you get acquainted with different areas of our knowledge base.

Once you have servers created and have learned the steps by migrating your first website over, it’s then super quick and easy to migrate more.

### Table of Contents

 

 

### Multisite Notice

If you're migrating in a multisite, be sure to toggle on the appropriate multisite setting in your website customizer BEFORE you begin. Learn more here:
How to Enable WordPress Multisite on GridPane

## Step 1. Create your server

If you don’t have a server prepared already, you first need to create your server within your GridPane account.

Creating your very first server will take a few minutes of your time to generate your API key at your chosen provider, or spin up your custom VPS.

Once you have what you need in place, server creation takes approximately 15 minutes. To get started, please check out this section of our knowledge base:

Provisioning Servers

 

## Step 2. Create your website

Once your server is live, you can now create your website. GridPane makes it super quick and easy to create new WordPress sites, and if you have a favorite migration plugin, you can add this to a bundle, so it’s already installed and activated when you login.

Here’s our knowledge base section for creating new WordPress sites (top left): Deploying GridPane WordPress Sites

Tip: Always leave caching turned OFF until you’ve successfully imported your website.

 

## Step 3. Provision your SSL certificate

Provisioning an SSL isn’t required when migrating, but you will need to set one up in advance in order to migrate with zero downtime. To accomplish this, we offer a few different ways to provision an SSL before changing your DNS records. The easiest method is to use our DNS API integration:

Provisioning an SSL for a domain using DNS API Domain verification

### If You Don’t Control DNS…

If you’re migrating a clients website over but don’t manage their DNS, check out how to provision an SSL via proxy challenge with Cloudflare here:

Provisioning an SSL for a domain using DNS API Domain verification by Proxy Challenge

### Additional Benefit

Provisioning an SSL before you import your site will set your site up to serve over HTTPS in advance.

### Further Info on SSL Certificates

An entire section of our knowledge base is dedicated to SSL certificates and GridPane here:

Provisioning SSL Certificates

 

## Step 4. Export your website

There are many different ways to migrate a website, but we’ve had great success with and recommend All in One WP Migration and Migrate Guru. With these two plugins, we’ve migrated 50GB websites, and seen 400+ subsite WaaS networks be successfully transferred to us.

Here’s our knowledge base section on migrating to GridPane, and here there are also guides for manual migrations:

Migrating Websites to GridPane

Tip: Clear and disable the cache before exporting your site to prevent unusual behavior when you import the site into GridPane.

 

## Step 5. Connect to your website over a local hosts redirect

You can connect to your website without needing to change your DNS records over by editing your local hosts file. This is an excellent tool for your web hosting toolkit, and we highly recommend you take advantage of this when migrating websites from one place to another. Using a local hosts redirect, you can log in and edit your websites and ensure that everything is working correctly before switching the DNS over and setting them live to the world.

Here is our knowledge base article on how to edit your local hosts file:

How can I edit my local hosts file to redirect URLs

 

## Step 6. Import your website

Import your website using your preferred method.

Our knowledge base articles for migrating to GridPane detail both the exporting and importing parts of the process:

Migrating Websites to GridPane

 

## Step 7. Setup SMTP and check your contact forms

If you don’t already use an email service to send your website’s transactional email, you’ll need to connect a mail service such as SendGrid, Mailgun, Postmark, Sendinblue, Amazon SES, etc. GridPane has a SendGrid integration which, once you’ve entered your API key, you can simply toggle on for any of your websites.

You could also use the excellent and free Fluent SMTP plugin to easily connect to a variety of different mail services.

Here’s our knowledge base for our SendGrid integration:

SMTP and Transactional Email

 

## Step 8. Confirm all is well and switch your DNS to point to GridPane

Once you’ve migrated your website over and have made sure everything’s working correctly. You can now switch your DNS to point to your GridPane server.

Setting DNS Records

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

