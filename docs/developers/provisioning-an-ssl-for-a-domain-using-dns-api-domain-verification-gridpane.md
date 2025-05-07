# Provisioning an SSL for a domain using DNS API Domain verification | GridPane

# Provisioning an SSL for a domain using DNS API Domain verification

 

7 min read 

### Table of Contents

 

## Introduction

This article will explain how to add an SSL Certificate from the free Let’s Encrypt Certificate Provider with GridPane using one of our DNS API integrations. This will allow your site to be served by the encrypted HTTPS protocol, and your visitors will also benefit from the speed increased enabled by HTTP2 which only works via HTTPS.

Using the DNS API integration method requires your domain to be managed by one of the DNS management services we GridPane integrates with. We currently support two of the biggest DNS management services:

Using the DNS API integration method does not actually require any DNS records to point to the IP of the server hosting the site, which makes it perfect for provisioning SSLs during migrations or for testing before DNS changeover.

GridPane does not enable/disable SSL for the site, but rather it manages SSL on a per-domain basis for each domain attached to a site. This means SSL management is done through the domains tab.

In this Knowledge Base article, we will use a site’s primary domain to demonstrate, however, the same functionality and process is true for any added Alias and Redirect domains.

 

 

### IMPORTANT

If you change your DNS API key you must replace the old key inside your GridPane with your new one to ensure that your Acme provisioned SSL certificates will be able renew successfully. If your API key is incorrect, Let's Encrypt will not be able to renew your SSL certificate, and if your SSL expires you will experience HTTPS issues that could make your website inaccessible or throw warnings.

## Sign up for an account at a DNS Provider

To use a DNS API integration to provision an SSL with GridPane, you will need to have an account with one of the supported DNS providers.

If you haven’t already you can sign up here:

 

## Copy Your DNS API Keys

### Copy your Cloudflare API credentials

Log into your Cloudflare account and add a site to be managed or select an already managed site, then go to the overview page:

Then find the API section near the bottom of the page on the right section of the page.

Click Get your API token:

In the API section, copy your account email address from the Communication tab:

Then Click the API Tokens tab, and click View for the Global API Key:

Copy your API Key:

### Copy your DNSMadeeasy API credentials

Log in to your DNSMadeeasy account and then go to the account information page.

Copy the API Key and API Secret from the bottom of the account information page:

 

## Store Your DNS Provider API Keys in GridPane

Now we need to enter your DNS service API credentials into your GridPane settings.

Navigate to your GridPane Settings page:

From the left-hand side menu, click through to “Integrations” and then “DNS Providers“:

Select DNS Made Easy or Cloudflare, and click the “New DNS Made Easy Integration” or “New Cloudflare Integration” button.

Here you can enter your API credentials in their respective input fields and click Add:

Your credentials will now be saved in your GridPane settings, and you can sync, edit, or delete your credentials using the buttons on the right-hand side:

### If you are using Custom/Vanity nameservers at your DNS provider

If you are using custom/vanity nameservers at your DNS provider, you will need to add these to your GridPane DNS API settings for that provider.

Click on the Nameserver Domain accordion dropdown for your DNS provider:

You will only need to enter the root domain of your nameservers. So if your nameservers are ns1.gridpane.com and ns2.gridpane.com then you will add gridpane.com and click create.

 

## Step 1. Open the Site Customization Panel for your Active site

Click on the sites link in the GridPane main menu to go to the Sites management page:

In the Active Sites panel, click on the domain in the URL column to open the Site Customization pop up box for the site you wish to update:

 

## Step 2. Ensure Domain API Integration is set to Full

Open the domains manager tab of the site customizer:

If the API Integration of the domain you wish to enable an SSL for is set to None then click on the grey None box:

This will open a modal window where you can choose either Cloudflare Full or DNSME Full to use DNS API domain verification for your SSL provision:

Once you have selected the DNS API Full integration it should show in a green box on the domain row.

Cloudflare full:

DNSME Full:

 

## Step 3. Enable SSL

Locate the SSL toggle for the domain that you wish to provision an SSL for:

Toggle it on and the settings modal will open.

This will present you with options to do a dry run (recommended) and select if you want to “Include Database Rewrites”:

Generally, you’re going to want to run database rewrites. This will run a search and replace and ensure that all of your URLs are set correctly for your routing and HTTPS.

Two options are available to you:

InterconnectIT is usually the best option as it’s more comprehensive. WP-CLI maybe a little quicker, but has a higher chance of missing some rewrites.

Make your selection and hit the Enable SSL button.

GridPane will begin provisioning SSL for your site’s domain. You will see Notifications pop up in the top right corner of your browser as the SSL attempts progress:

Enabling an SSL can take some time, especially when using the DNS API method. Expect the SSL attempt to take several minutes.

You can keep track of the notifications as they inform you about the progress of the SSL attempt. Alternatively, you can check the SSL provision log, available from the logs tab of the site customizer. The SSL provision attempt outputs every step of the process to the log:

 

 

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

