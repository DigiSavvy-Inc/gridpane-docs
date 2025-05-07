# Using GridPane AutoSSL | GridPane

# Using GridPane AutoSSL

 

5 min read 

### Table of Contents

 

 

### Information

If your website is not a multisite/WP-Ultimo website, AutoSSL is not necessary for your website.

## Introduction

GridPane AutoSSL automatically attempts to provision an SSL for any domain that is added to a GridPane-managed site. It will begin first with the site’s primary domain, before moving on to provision SSL for all other attached domains. Here’s a breakdown of how this function works:

##### Failed SSL Attempts

If the SSL attempt for the primary domain fails, then AutoSSL stops there and is set to OFF. No attempts will be made to enable SSL for any of the other domains once the primary domain SSL attempt fails.

If, however, an SSL attempt for any of the additional domains fail as part of the AutoSSL process, it will only affect that domain. The AutoSSL process will continue on until an SSL attempt has been made for all attached site domains.

##### AutoSSL and the Primary Domain

If you have AutoSSL set to ON for your site, but decide to disable the SSL for your primary domain via the domain manager, then it will also disable AutoSSL.

##### Disabling AutoSSL / SSL Certificates

Disabling AutoSSL does not disable all the SSL for all domains on your site, instead it just stops AutoSSL going forward. If you want to disable ALL SSL for your domains, you will need to turn each domains SSL off individually.

 

### What AutoSSL is Not

The name “AutoSSL” is often confused to mean this option automatically always makes sure an SSL is provisioned for your websites. This is not AutoSSL’s intended function.

Once you provision an SSL for any website, regardless of whether you use AutoSSL or just use the regular toggle inside the domains tab in your website customizer modal, our systems will automatically attempt to renew your SSL certificates every 60 days. If, for any reason, this fails, your server will re-attempt to renew every day for the next 30 days until it expires. Each failed renewal attempt will result in a notification inside your dashboard, giving you plenty of time to resolve the issue.

 

## Enabling AutoSSL

Enabling AutoSSL is a simple process.

### Step 1. Open the Website Customizer

Click on the sites link in the GridPane main menu to go to the Sites management page.

In the Active Sites panel, click on the domain in the URL column to open the Site Customizer for the site you wish to update:

### Step 2. Enable AutoSSL Toggle

Locate the AutoSSL toggle in the list of site customizations available and click the toggle from OFF to the ON position:

GridPane will begin provisioning SSL for your site’s attached domains. You will see Notifications pop up in the top right corner of your browser as the SSL attempts progress.

As each SSL attempt proceeds successfully, the domains in your domains tab will have their SSL toggles enabled:

If you add any new domains while AutoSSL is enabled, they will automatically provision enable SSL once the domain has been added.

Enabling an SSL can take some time, especially if you are using any DNS API integration method. You can keep track of the notifications as they inform you about the progress of the SSL attempt. Alternatively, you can check the SSL provision log, available from the logs tab of the site customizer. The SSL provision attempt outputs every step of the process to the log.

 

 

## SSL Support

SSL Certificates Failures
For assistance with SSL certificate related issues, please ensure you attach the info from your SSL provisioning logs when contacting support/posting in the community forum so that we can quickly assess what's going on and assist you as fast and efficiently as possible.
How to Create a Support Ticket
DNS Checks / Console Output / Screenshots
Please provide as much relevant information as possible - check if your DNS is live,  check console output on your site (right click > inspect element > console), and attach any relevant screenshots of errors.

Too Many Redirects Error
If you're using Cloudflare with GridPane, please ensure you have the correct SSL settings to prevent redirect errors:How to use Cloudflare SSL with GridPane
SSL Locks and Rate Limiting
If multiple SSL attempts fail, GridPane will place an SSL lock to prevent you from getting rate limited by Let's Encrypt. It's important to assess why your SSL's are failing and correct the issue. Learn more about rate-limiting and how to remove locks here:GridPane SSL Locks and Let’s Encrypt Rate Limiting
SSL Troubleshooting Guide
This article will help new users prevent common SSL issues, and learn how to diagnose the more complex ones.
Diagnosing and Fixing SSL Certificate Issues
SSL Renewal Failures
If you're receiving notifications that one of your SSL certificates has failed to renew, Let's Encrypt will return the exact reason for failure inside the Certbot or Acme monitoring logs.

Monit SSL Renewal Failure Notification in the Dashboard or Slack
Mixed Content / No Padlock
If you've provisioned an SSL but don't see a padlock, please check for images and/or other content being served over HTTP instead of HTTPS. It's likely you need to update your database to serve links over HTTPS:
Why Am I Not Seeing a Padlock on my Site?

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

