# New WordPress Website Build Configuration Settings | GridPane

# New WordPress Website Build Configuration Settings

 

5 min read 

GridPane simplifies the process of deploying new WordPress sites in a much more secure manner than the traditional WordPress 5 Minute Installation.

With your account, you the ability to set the default configuration settings for new WordPress builds, and this includes things like your preferred caching options, WAF options, whether or not to activate the SendGrid SMTP API integration, whether or not to automatically provision an SSL and more.

This article will walk you through how to set this up.

 

## Step 1. Navigate to the settings page

To get started, login to your account and click on your name in the top right-hand corner, and then choose the settings option from the drop-down.

Next click on Default WP Build Settings in the menu on the left hand side.

 

## Step 2. Choose your site build settings

Here you’ll see the following list of settings that you can configure as the default when you create new WordPress websites.

 

### System User

You have the option to autocreate a new system user, create a new user (choose the name), or choose to select an existing user. We strongly recommend you use a separate system user for each individual website. This ensures that:

 

### WordPress Admin Users

 

### Bundles

Do you have a bundle that you use on all or most of the new websites you create? You can now choose to set one of your bundles as the default option.

You can check out how to create new bundles here: Using GridPane Bundles.

 

### PHP Version

Choose your preferred PHP version.

 

### SMTP Integration

We currently have an API integration with SendGrid’s SMTP service. If you’ve set your API key, you’ll have the option to choose to activate the SMTP integration automatically as new sites are created.

You can learn how to setup the SenGrid integration here: Using SendGrid SMTP for Transactional Emails.

 

### SSL

You have the option to provision an SSL for your websites automatically once they’ve been created. This will take place immediately once the install has finished being set up and the website is ready for use.

You have the option to choose AutoSSL (good for multisites and sites that will have multiple different domain names attached to them), Primary Domain SSL (suitable for regular websites), or None (best if you haven’t set up your DNS records or a DNS API integration).

You can learn more about provisioning SSL certificates for your websites here: Provisioning SSL Certificates.

 

### DNS API Integration

GridPane has DNS API integrations with Cloudflare and DNS Made Easy. If you’re using one of these services and have set up your API key, you can choose to set that integration as your default.

The available options are: –

You can learn about setting up DNS integrations here: –

 

### Git Integration

If you have a standard Git integration for the sites you regularly build you can set this and the branch as the default.

 

### Local Backups

We recommend local backups (stored directly on your server) for recovery on your sites:

 

### Remote Backups

Choose your preferred provider and set your backup and retention schedule.

 

### Advanced Options

You have the option to create a staging site and a canary site for each of your websites. Staging is great for making changes and testing updates to make sure they all work correctly before you run them on your live site. This keeps them safe and up and running.

Canary sites are for our UpdateSafely feature. This is currently being refactored for re-release in the near future and isn’t operational at this time.

You can learn about staging sites here: Using staging sites on GridPane.

 

## Step 2.1 Nginx Site Settings

### PHP Process Management

Here you can choose the default option for how your PHP workers are set on your new websites. If you’re unsure, we recommend you stick with the default option and leave it as “Dynamic“. You can choose to set them as Static, Dynamic, or Ondemand.

To learn more about PHP workers and how to change their settings on your GridPane servers, check out this section of the Configuring PHP: PHP by Site – Process Manager/Workers.

 

### Nginx Caching

Set your preferred default caching option.

You can learn more about our caching options here: An Introduction to GridPane Server Caching Options.

 

### WAF on Nginx Sites

WAF stands for “Web Application Firewall”. GridPane has two deep integrations with the 6G WAF, 7G WAF, and ModSecurity.

We recommend 7G for most websites.

 

## Step 2.2 OpenLiteSpeed Site Settings

### PHP Process Mode

Unless you have a very specific use case, leave the default setting as ProcessMode:

 

### OpenLiteSpeed Caching

OpenLiteSpeed comes with LS Caching and Redis Object caching. We recommend both for most websites:

 

### WAF on OpenLiteSpeed Sites

The older 6G WAF is only available on older Nginx stacks. We recommend 7G for most websites:

 

## Step 3. Save your settings

Once you’ve set your preferences simply hit the update button and you’re all set.

Now when you go to create a new website, your default options will be pre-selected for you, and you can adjust as necessary for new sites that need a slightly different configuration.

You can also reset them anytime by clicking the “Reset to GridPane Default” at the top of the settings any time.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

