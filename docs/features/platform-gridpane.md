# Platform | GridPane

 

## GridPane Platform Documentation

 

Below you’ll find the documentation for every feature inside the GridPane UI, as well as documentation that directly compliments these features. Each area is broken down by page and then by category to make it easy to navigate and find what you’re looking for.

 

Create a New Server

GridPane offers two methods for creating servers. The first is by simply generating an API key at one of the 5 providers we integrate with, and the second is the custom option which allows you to connect any high quality VPS or dedicated server from a reputable provider.

Here are the articles on how to get started (listed in no particular order):

We generally recommend getting started with any of the above except for Lightsail, who heavily restrain the

For more information on using the custom option we have server articles on how to do this with various providers including Google Cloud, AWS EC2, Hetzner, Katapult, and OVH. You can learn more here:

There’s no difference in how our stack operates on API created servers vs custom servers.

Server Customizer Settings

The server customizer contains various options to change the settings on your servers. To open the customizer, simply head to the Servers page click on the name of your server. Here you’ll find:

Settings

UpdateSafely™ (BETA)

BackupsIn the backups tab you can set the daily pruning time and backups concurrency:

Nginx

The Nginx tab allows you to activate/deactivate GridPane Nginoil:

PHPSettings coming soon.

MySQLThe MySQL tab allows you to activate MySQL slow logging, and also allows you to restart MySQL as well.

RedisSettings coming soon.

Server LogsThe Logs tab contains your server logs, and this is a tab you’ll want to become familiar with. Here’s a breakdown:

Monit: View Your Server Stats

All GridPane servers comes configured with Monit, an open source tool that comes complete with all the features needed for system monitoring and error recovery. It is an incredibly lightweight Open Source utility for managing and monitoring Unix-like systems. Monit conducts automatic maintenance and repair and can execute meaningful causal actions in error situations.

Learn more about Monit and how to open it here:

Add or Remove SSH Keys

Learn how to create and add SSH keys to your account, and how to add and remove keys from individual servers:

Rename / Delete / Reboot a Server

Next to your servers is a series of 3 or 4 buttons next to your servers. As well as adding/removing SSH keys, you can rename, reboot, or a delete a server from your account.

Rename a ServerNot all providers allow for renaming your servers, so you will only see the rename icon if that provider allows for this:

Delete a ServerIt’s important to note that if you an API key provisioned server, our system will also delete it at the server provider. Custom provisioned servers will need to be manually deleted:

Reboot a ServerIf you need to reboot a server for any reason, it’s as simple clicking the power icon button.

Create a New WordPress Website

GridPane simplifies the process of deploying new WordPress sites in a much more secure manner than the traditional WordPress 5 Minute Installation. You can also set your default preferences so these settings are pre-configured each time you create a new site.

Access PHPMyAdmin

GridPane offers 1-click login access to PHPMyAdmin (PHPMA) for all of your websites.

Single Sign-On (SSO)

GridPane allows you to login to your WordPress websites with 1-click:

###### Website Customizer

 

To open up the website customizer, simply navigate to the Sites page in your account and click on the name of the website. The majority of your website settings can be found here.

 

Website Settings

When you open up the website customizer you’ll first see the Settings tab. Here you can do the following:

On OpenLiteSpeed you can also activate LiteSpeed page caching and Redis Object Caching in this tab.

Caching Settings

The Caching tab will show for Nginx servers and contains the settings to activate/deactivate either FastCGI or Redis page caching, and Redis object caching.

Details on adjusting TTL is detailed in the above articles.

WordPress Security Settings

GridPane offers a lot of security out of the box as well as a suite of tools to lock your websites down. This article offers introduction to the Security tab:

The following articles detail each of the options you’ll find here:

Additional Note: You can only activate one Web Application Firewall at a time. We generally recommend 7G for most websites (over 6G),  and it’s a great, lightweight firewall that is easy to customize. ModSecurity can be a great upsell to your clients who want the most secure option available.

PHP Settings

Your PHP INI, PHP-FPM (Nginx), PHP LSAPI (OpenLiteSpeed) settings can all be configured directly within the website customizer in the PHP tab. Here you can also change your website’s PHP version as well.

Configure PHP INI Settings

PHP WorkersPHP-FPM and PHP LSAPI are your PHP worker settings. You can learn more about PHP workers in this in-depth article:

PHP Slow LogPHP slow logging is currently available on Nginx servers:

WordPress Website Backups

GridPane offers one of the most comprehensive WordPress backup systems available.

Our documentation is broken down into three parts:

We also have this article on our recommended backup strategy:

Website Cloning

GridPane makes cloning a website extremely easy. This includes cloning from one server to another and one website URL to another.

If you’re on the Developer plan or above, you can also clone one website OVER another existing site:

You may also want to read this article on working with the wp-config.php file on GridPane:

Manage Domains and SSL Certificates

The Domains tab is where you can provision SSL certificates, create Alias and Redirect domains, routing, and run domain swaps.

SSL Certificates

Alias and Redirects

Routing

Domain Swaps

View Your Website Logs

Your website logs are incredibly important, and you’ll need to know where they are and what they do. This article has the full rundown:

You can also enable WP_Debug and install the query monitor for your website in one click:

Multisite Settings

Enabling WordPress Multisite on GridPane is a quick and painless process. There’s no need to open and edit your wp-config.php file, all you need to do is click a toggle.

This article will walk you through how to find it and give you a little information on which multisite option (subdomain or sub-directory) may be the right one for your website.

Working with GridPane Staging

GridPane offers a comprehensive Staging <> Live system. For those on the Developer plan and above, you can also make advanced pushes that includes selecting specific database tables.

Access PHPMyAdmin

Like your live websites, you can also access your staging databases via PHPMyAdmin.

Canary Websites and UpdateSafely

UpdateSafely™ is our trademarked WordPress update system. This new 2.0 version (still currently in beta) has been recreated from the ground up and is designed to take care of a big part of your WordPress maintenance routine so that you no longer have to. Learn more here:

Create and Manage System Users

The following article details how to add a new System User to your GridPane account:

The following articles offer further information on working with System users:

Self Help Tools

The Tools page contains several useful tools that make several common hosting tasks extremely easy to do directly within your account.

Here you’ll also find the server to server cloning tool. This will clone all of your production sites (not including staging or canary).

Snapshot Failover™

Snapshot Failover™ is an excellent feature to be able to offer as a part of your hosting service. It’s impressive to clients, takes relatively little effort, is relatively inexpensive if you’re taking the cost into account in your offering, and it also provides you as the service provider some peace of mind.

A second server is also a second set of backups, which is never a bad thing either.

An article for Cloudflare will be coming in the near future, but any DNS provider that can monitor one server and then switch DNS records over to a second server if it sees the first server go down will work.

Full and Hybrid Git Repositories

The Git page contains all of the documentation for using our Git integration. This includes both Full and Hybrid Git repositories.

GridPane Multitenancy

Unlike the standard Git integration, when using multitenancy, you set your Git repo once inside the server customizer, and it automatically applies to every website created on that server. This means there’s one immutable codebase for all individual websites, and when you push updates via Git, they apply to all websites on that server.

Support

To ensure that our team can help you as efficiently as possible, please provide as much relevant information as possible in your first message. This includes your logs, troubleshooting steps you’ve already taken

GridPane is self-managed hosting, not managed, and you will need to do your part in troubleshooting.

For Panel accounts (and for most general issues for other accounts), support starts in Community Forum and, if necessary, we’ll create a support ticket for you.

Our team is active in the forum all day every day.

Profile Settings

The first tab in the Settings page is your profile tab. Here you can change your account email address, account profile picture, and time zone.

The time zone is important as it will ensure your notifications display the correct timestamp for your location. Learn more here:

Teams

GridPane allows you to create teams to help you manage the websites that you host, and/or give your clients access to manage their own websites. This article breaks down how it works and the different options available to you.

Security

Inside Security in your Settings page, you can change your password and enable 2FA.

GridPane API

In your Settings page in GridPane API you can create your own personal access token and regenerate the GridPane API token.

The API is still beta and is being actively developed. This article provides an intro for getting started:

SSH Keys

Adding your SSH Keys to GridPane is quick and easy, and you can set default keys so that they’re automatically added to newly created servers (you’ll still have to push them to existing servers).

If you have trouble adding your SSH key, see this article for troubleshooting steps:

Integrations

Here you can add your API keys for the various services that we integrate with.

Cloud ProvidersDetails for cloud providers can be found in their provisioning docs:

DNS Providers

Backup Providers

SMTP Providers

More coming soon.

Default Server Build Defaults

The default server build settings are all self-explanatory. Here you can set how the following will automatically apply to newly created servers:

Learn more about these settings here:

Default WP Build Settings

You can set both your default WordPress administrator account settings and the default configuration settings for when you create new sites here.

 Default UpdateSafely Settings

UpdateSafely™ is our trademarked WordPress update system. This new 2.0 version (still currently in beta) has been recreated from the ground up and is designed to take care of a big part of your WordPress maintenance routine so that you no longer have to. Learn more here:

Slack Notifications

We highly recommend that you enable Slack notifications for your account, and this article will get you up and running:

You can also learn more these notifications here:

Immutable Blueprints

Immutable Blueprints are specifically for our multitenancy feature. This currently has no public documentation and is only available at the Agency tier.

Bundles

GridPane Bundles let you preconfigure your GridPane WordPress site deployments with the Plugins and Themes installed that you most commonly used.

You can create many different types of Bundles to suite the different types of projects that you work on. This is our doc on getting started:

For themes and plugins that are not available on the WordPress repository, you can still use them with Bundles if you self-host these. Here’s how to do so with Dropbox and Google Drive:

Onboarding

Here you can view our onboarding videos directly in the application. These are also available here in this article:

More videos will come in the future.

Addons and Preemptive Support 360

Addons allows you to enable our GridPane 360 Preemptive Support service on your servers.

Preemptive Support allows you to manage enrolled servers.

Learn more about 360 here:

Billing

The Billing section inside your Settings page allows you to:

If you have an issue with Billing you can reach out to us on Support and we will get back to you ASAP.

Table of Contents

