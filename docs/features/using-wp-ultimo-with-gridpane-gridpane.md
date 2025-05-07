# Using WP Ultimo with GridPane | GridPane

# Using WP Ultimo with GridPane

 

9 min read 

## Introduction

WP UItimo is a popular plugin for creating a WaaS (website as a service) website. This guide will walk you through the steps needed to set up your WP Ultimo site on GridPane. The same steps apply whether it’s brand new or if you’re migrating your website over from another host.

### Table of Contents

 

 

### Note

With the exception of legacy accounts, WP Ultimo is not supported on our Pro (no-longer available for sign-up) or Panel level accounts. If you require support, please upgrade to the Developer plan.

## How it Works

We’ve worked closely with the developer of the WP Ultimo plugin to fine-tune the way our platform and UI integrate together. Once activated, our integration allows the domains you or your customers map inside of Ultimo to automatically create an SSL certificate. Pretty cool right? Let’s get started.

For the remainder of this article, we’ll also be using the $0.99 bargain domain name “waas.monster” for illustration purposes.

 

## Part 1. Setting Up Your WP Ultimo Website in Your GridPane Account

### Step 1: Setup Your Server

If you haven’t already set up your server, please check out this section of the KB:Provisioning Servers.

There are a few considerations you may want to keep in mind when choosing your server:

### Step 2: Create your website and choose a DNS integration

First, be sure to add your domain to either your Cloudflare or DNS Made Easy account and add your API key to your GridPane account. Here are our KB articles for how to do this:

At this time, the staging and canary won’t work with a multisite, so you can uncheck them. I’ll be creating waas.monster with the Cloudflare API (make sure whichever you choose is set to “Full”). If there are going to be other websites on this server (not recommended), then make sure they are owned by a different system user.

Note: If you’ve already set up your domain without a DNS integration, you can click on the domain name in your account to open up the configuration modal, then click on the domains tab. Once here, click on the box below the API integration to:

### Step 3: Enable Multisite on your website

Open your website’s configuration modal and click on the “Multisite Settings” tab. Here we have two options:

It’s important to choose the correct one right off the bat. WP Ultimo will work with both options. The difference between the two is how the URL structure is set up. Below is an example for each:

If you’re importing an existing WP Ultimo site, then please choose the one which you already use. If you’re converting an existing regular/non-multisite WordPress website (that already has published content) into a multisite, then the subdomain is the better choice.

As GridPane doesn’t put any restrictions on subdomains, you’re free to choose whichever option you prefer. For waas.monster, I’m going to select the subdomain option.

### Step 4: Provision a Wildcard SSL Certificate

Now that your website is up and running and integrated with either DNSME or Cloudflare, you can now provision a Wildcard SSL. At the moment, with the wildcard toggle for your domain toggled to off, the domain is configured as a standard Nginx virtual server.

This means that the server is configured to serve yourdomain.com and www.yourdomain.com (all GridPane domains are automatically configured to include the www host domain).

For the server to be able to serve all subdomains of your root domain via a wildcard configuration, you will need to reconfigure Nginx – luckily, that is just a toggle away 🙂 First, set up your website for a WildCard SSL by toggling it on in the domains tab of your configuration modal.

Your website has now been configured. Next, toggle on SSL to provision your SSL certificate, and you’re then set to move on to the next step. Please note that a Wildcard SSL can sometimes take 5-7 minutes so please be patient while it runs.

For a more detailed rundown of provisioning a Wildcard SSL, check out:

Provisioning a Wildcard SSL for a domain using DNS API Domain verification

### Step 5: Turn on AutoSSL

GridPane AutoSSL automatically attempts to provision an SSL for any domain that is added to a GridPane-managed site. As we’ve already provisioned our SSL for our primary domain, once toggled on, AutoSSL will remain ON, and for any domains that you now add to your WP Ultimo site, GridPane will automatically attempt to provision an SSL. You can enable AutoSSL in the settings tab:

For a more detailed rundown of how AutoSSL works, check out:

Using GridPane AutoSSL

### Wrapping Up Part 1

And that’s it for part 1. Your website is now ready for WP Ultimo. If you’re importing an existing Ultimo site, then you can now proceed to do so.

For this, the Migrate Guru plugin is an excellent, reliable solution, and we’ve seen it work on HUGE Ultimo sites with great success (although it can take some time to run). We have this handy guide on how to use Migrate Guru:

Migrate Sites to GridPane using Migrate Guru

The All in One WP Migration (AIOM) Multisite Extension plugin is also a great choice, though it’s not free. Here’s our knowledge base article for using AIOM:

Migrate Sites to GridPane using All in One WP Migration

If you’re migrating an existing WP Ultimo site, then please skip Part 2 and proceed to Part 3.

 

## Part 2. Setting Up WP Ultimo On Your Website

### Step 1: Install WP Ultimo

Login to your website and navigate to Network Admin > Plugins:

WP Ultimo needs to be activated network-wide. Upload your plugin, and click Network Activate.

### Step 2: Proceed to Step 2 (System) in the Setup Wizard

Once activated, it will bring you to the setup wizard.

Here we need to click through to step 2 (System) where it copies the Sunrise file into wp-content.

You may skip step 1 (Settings) for now if you wish.

At step 2, click the “copy automatically” button under step 1. Copying sunrise.php.

Note: You may skip “2. Setting SUNRISE to true” as our integration will take care of this during part 3.

As soon as you’ve clicked the copy automatically button, you’re ready to proceed to Part 3.

 

## Part 3. Complete Your WP Ultimo Integration Setup

IMPORTANT: If you haven’t completed step 2 and copied the sunrise file into wp-content, our integration will not work until sunrise.php is in the correct location.

 

 

### Pro and Panel Account Notice

The Ultimo toggle below and support for Ultimo sites is only available to Developer level accounts and above.

If you are a Pro or Panel plan user and wish to use our integration, we have added the GP-CLI command that will allow you to do so below, however, support for Ultimo sites is a developer level feature.

### Step 1: Toggle on the WP Ultimo Integration

Inside your websites configuration modal, click through to the Multisite settings tab and click the toggle to on.

Your GridPane-Ultimo integration is now complete.

The GP-CLI for activating our Ultimo integration is detailed below. Pro and Panel users, please ensure you have read and understood the notice in the green box above.

On your server, enter the following (replace site.url with your domain name):

```
gp site site.url -gp-ultimo-on
```

You can also deactivate it with:

```
gp site site.url -gp-ultimo-off
```

### Step 2: Disable Clickjacking [Optional]

Disabling clickjacking is necessary for the Ultimo templates option to function correctly.

If you need this feature, open up your configuration modal, and in the settings tab, toggle the Clickjacking Protection toggle to “OFF“:

### Step 3: Add any domains that were added to your Ultimo site prior to our integration

Once our commands have been run, any mapped domain name that you add to your site from here on out will now automatically be added to the domains tab, and AutoSSL will automatically provision at SSL for them.

For those of you who have migrated your Ultimo site into GridPane, or that have mapped any domains prior to our commands being run, you will need to add these manually to your primary domain’s configuration modal.

To do this, click on the green “Add Domain” button:

Add your domain name, select “Alias”, and from the “provider” dropdown, you can select an API integration if you wish to do so.

Once you’ve added your existing domains, your Ultimo site is now fully integrated with GridPane.

 

## BONUS: Part 4. Domain Mapping and Adding Alias Domains

To allow your clients to use their own domains on their websites, you need to activate domain mapping on your Ultimo settings page. Navigate there and select the following two options:

Sidenote: You may also want to select the SSL options a little further down.

With these enabled, when you or your client add an alias domain to a subsite, it will automatically get added as an alias in your website’s domain tab. If you have autoSSL enabled, it will then immediately attempt to provision an SSL certificate.

If you want to add an alias domain to one of your subsites, you can do this by navigating to:

Network Admin Panel > Sites > Click EDIT on the site > Click the Aliases Tab.

Here you can enter the domain and click save. Once that’s done, you’re all set.

Your clients can also do this themselves via their Account page.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

