# Provisioning an SSL for a domain using Webroot Domain Verification | GridPane

# Provisioning an SSL for a domain using Webroot Domain Verification

 

4 min read 

### Table of Contents

 

## Introduction

This article will explain how to add an SSL Certificate from the free Let’s Encrypt Certificate Provider with GridPane using webroot domain verification. This will allow your site to be served by the encrypted HTTPS protocol, and your visitors will also benefit from the speed increased enabled by HTTP2 which only works via HTTPS.

Webroot domain verification is the simplest method, but it requires that your GridPane site domain has DNS records pointed to the GridPane managed server IP.

GridPane does not enable/disable SSL for the site, but rather it manages SSL on a per domain basis for each domain attached to a site. This means SSL management is done through the domains tab.

In this Knowldege Base article we will use a site’s primary domain to demonstrate, however the same functionality and process is true for any added Alias and Redirect domains.

Note: Within this article we’re going to use an-example.site to illustrate things. When following along with this knowledge base article please make sure you substitute this string for your real domain name.

 

## Step 1. Ensure DNS records resolve to the server

We recommend having records for both the root domain and for the www host domain, for example:

```
an-example.site
www.an-example.site
```

For the root domain, you will need an A record set to the IP of the server.For the www  host domain  you can either use an A record or a CNAME record

For the webroot method GridPane currently checks for domain resolution directly to the server, this is both to avoid hitting any LE limits and to verify which domains resolve for grabbing the correct cert. GridPane will grab certs for whatever domains are possible, so if you forget your www record then the system will provision an SSL certificate without it.

You can check your domains dns resolution using any one of many online websites, or one of several command line tools.

 

## Step 2. Go to the Sites Section of the GridPane Control Panel

Click on the sites link in the GridPane main menu to go to the Sites management page.

 

## Step 3. Open the Site Customization Panel for your Active site

In the Active Sites panel, click on the domain in the URL column to open the Site Customization pop-up box for the site you wish to update.

 

## Step 4. Enable Lets Encrypt SSL for Your Domain

Open the Domains tab in the site customizer:

Locate the SSL toggle for the domain that you wish to provision an SSL for:

Toggle it on and the settings modal will open.

This will present you with options to do a dry run (recommended) and select if you want to “Include Database Rewrites”:

Generally, you’re going to want to run database rewrites. This will run a search and replace and ensure that all of your URLs are set correctly for your routing and HTTPS.

Two options are available to you:

InterconnectIT is usually the best option as it’s more comprehensive. WP-CLI maybe a little quicker, but has a higher chance of missing some rewrites.

Make your selection and hit the Enable SSL button.

GridPane will begin provisioning SSL for your site’s domain. You will see Notifications pop up in the top right corner of your browser as the SSL attempts progress.

Enabling an SSL can take some time.

You can keep track of the notifications as they inform you about the progress of the SSL attempt. Alternatively, you can check the SSL provision log, available from the logs tab of the site customizer. The SSL provision attempt outputs every step of the process to the log.

 

 

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

