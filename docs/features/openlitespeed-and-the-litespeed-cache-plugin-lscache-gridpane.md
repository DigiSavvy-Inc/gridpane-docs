# OpenLiteSpeed and the LiteSpeed Cache Plugin (LSCache) | GridPane

# OpenLiteSpeed (OLS) Caching and the LiteSpeed Cache Plugin (LSCache)

 

22 min read 

### Table of Contents

 

## Introduction

The LiteSpeed Cache plugin is one of the major reasons that both OpenLiteSpeed (OLS) and LiteSpeed Enterprise are so highly touted by the WordPress community. It is an exceptionally good plugin and with GridPane OLS you can take advantage of this for the websites that you host.

This article is intended as a getting started guide rather than an in-depth look at every one of the plugin’s extensive list of features. Many options within the plugin itself are self-explanatory and there are links to the official documentation in many areas as well.

We’ll look at getting a regular website set up properly, and explore some of the more interesting features that are available.

You can also find the official LiteSpeed Cache documentation for WordPress here:https://docs.litespeedtech.com/lscache/lscwp/

 

## The LiteSpeed Cache Plugin

The plugin will be pre-installed on the websites that you create, and if you’re cloning from Nginx, we will remove the Nginx plugins, and install the LSCache plugin. These swaps go both ways so if you migrate to Nginx, the LSCache plugin will be removed, and the Nginx plugins installed.

The plugin is developed and maintained by the team that create LiteSpeed (it is not a custom GridPane plugin), and you can find it on the WordPress repository here:

LiteSpeed Cache By LiteSpeed Technologies

 

## Activating OpenLiteSpeed Caching and Redis Object Caching

Just like our Nginx stack, OLS of course comes with Redis Object Caching. Both page and object caching can each be toggled on/off and off within the dashboard and doing so will automatically turn it on/off inside the LSCache plugin settings.

NOTE: The reverse is not true, however, and turning it off within the website will not deactivate the toggles within your GridPane account.

### Activate/Deactivate Caching in Your GridPane Account

Head over to the Sites page inside your GridPane account and click on the name of your website to open up the website customizer.

Here you’ll find the LSCache Page Caching and LSCache Redis Object Caching toggles:

Simply toggle them ON or OFF as per your website requirements.

### Page and Object Cache Plugin Settings

Once toggled ON or OFF the setting will be reflected inside your website in the Cache settings page of the plugin.

Page Cache:

Redis Object Cache:

 

## Part 1. Cache Settings

This is where you can configure your caching settings for your website. You can tune this further in the page optimization settings in part 6.  There are a total of 8 tabs, and an additional 9th if you’re using WooCommerce on your website. We’ll look at each one by one below.

The bulk of these settings have an explanation and/or link to further documentation on the official LiteSpeed knowledge base:

https://docs.litespeedtech.com/lscache/lscwp/cache/

 

### Configuration

When configuring your specific URIs etc caching settings within the boxes inside the plugin, it offers a couple of options for how specific you want to be.

To tell LiteSpeed to cache the exact string, end the line with “$“.

Add “^” to the beginning of the string to specify the beginning.

The examples below are taken directly from the official documentation here:https://docs.litespeedtech.com/lscache/lscwp/cache/

### Adding URI’s

/security/ssl//security/ssl/webroot/security/ssl/dns-api/blog/security/ssl/

The string /security/ssl/ will match all four URIs.

The string /security/ssl/$ will match #1 and #4 and because $ specifies the end of the string.

The string ^/security/ssl will match #1, #2, and #3 because ^ specifies the beginning of the URI.

The string ^/security/ssl/$ will match #1 because it specifies both the beginning and the end of the string for an exact match.

 

### [1] Cache

 

Here you can turn your page caching functionality on and off, and fine-tune the specifics of what you do and don’t cache.

You can also configure caching for specific URIs and query strings. This can be a very handy feature, and the LSCache plugin makes this easy to manage directly inside of your website.

 

### Enable Cache

As mentioned earlier, toggling this on within the dashboard will automatically turn the Enable Cache setting to ON.

### Cache Logged-in Users

If you’re developing or designing pages within your website, turn this setting OFF.

Privately cached pages are stored in a private cache by IP and session ID, so individual users have their owned cached pages – it’s not simply serving a cached version of the page when logged in. If you have a use case for this, then turn it ON. For most websites, you’ll probably leave this setting OFF.

### Cache Commenters

Setting this to ON means that anyone who’s left a comment will not be able to see that their comment is under moderation and will be served the cached version of the page.

If you’d prefer that your commenters can see that their comment is awaiting moderation, you can set this to OFF.

### Cache REST API

The default ON setting is likely fine for most use cases, but always be sure to test it thoroughly to make sure.

### Cache Login Page

LiteSpeed states: “This option will cache the login page. Normally, there is no reason to uncheck this option. However, if there is something that may identify a user on the page, this should be off.”

If leaving ON just be sure to test logging in to make sure you’re experiencing any issues. If leaving OFF, be sure to activate Fail2Ban inside your website’s security tab to prevent brute force attacks.

### Cache favicon.ico

Keep this setting ON.

### Cache PHP Resources

Keep this setting ON for most websites.

This is for the OpCache and it will cache precompiled script bytecode for faster load times (usually known as Zend OpCache in PHP).

When developing leave this OFF.

### Cache Mobile

Leave this setting OFF unless your website isn’t using responsive design, or if your pages are significantly different, loading different resources/widgets/content on mobile.

### Private Cached URIs

If you have a lot of users that spend the bulk of their time logged in and visiting specific pages – for example a small LMS – this feature may be worth experimenting with. However, if you don’t have a specific use case where logged individuals would benefit from caching, leave this empty.

### Force Cache URIs

URIs added here will be cached regardless of any settings that try to prevent it.

### Force Public Cache URIs

URIs added here will be cached publically regardless of any settings that try to prevent it.

 

### Drop Query Strings

This is a great feature. It allows you to drop specific query strings and serve a cached version of your page (instead of the default behavior which is to BYPASS the cache).

This means for all Facebook links, and any other query strings specifically for marketing/analytics, the cached version of the page can be served, and the query string itself is still retained and can be tracked as per usual.

For any query strings that don’t affect the content displayed within the page, you can add them to this box (1 per line) and save your server from having to generate the page from scratch each time.

 

### [2] TTL

 

TTL stands for Time to Live,  and this is the length of time that your pages will be cached for. The default is 1 week for all front-end pages, and 30 minutes if you’ve set the cache to ON for logged-in users.

These defaults will work well for most websites.

### Default Public Cache TTL

For sites that are mostly static, you may want to increase this time to 30 days. For sites that publish a lot of content or receive a lot of comments, a shorter time may work better for you. Fine-tune as per you’re requirements.

### All Other Settings

If you have a use case where it makes sense to change these settings, adjust as per your requirements. If you’re not sure, leave the settings as they are.

 

### [3] Purge

 

Here you can configure how and when your site will automatically purge the cache for your website’s pages.

### Purge All On Upgrade

This will purge the entire cache anytime you run a core, theme, and/or plugin update.

This is generally a good idea for most websites, especially if you use a page builder of any kind.

### Auto Purge Rules For Publish/Update

Depending on how you’re website is set up, publishing new content may also update existing pages such as the home and archive pages. Here you can configure which pages/archives should be purged when you hit publish.

The All Pages option may be overkill for many of your websites. This option will of course purge the entire cache. For your typical brochure style website you may want to leave this unchecked. For websites where you publish a lot of new content regularly, this may be work well for you when combined with the setting below.

### Serve Stale

This option allows you to configure your caching to work in a similar manner to how our FastCGI caching works on Nginx.

If turned ON, once a page’s cache expires the server will still serve the previously cached version of the page as STALE to the next visitor that comes along, and then update the cache to the latest version of the page in the background so that the next person then sees the most up-to-date version.

This is great when, as mentioned above, you publish a lot of content regularly or get a lot of comments on your blog posts.

If you don’t have a specific need for it, it may be better to leave it turned OFF.

### Scheduled Purge URLs

Use cases for this are pretty rare, but if you need any specific URIs to be purged each day then this is a handy feature. List them in the box, 1 per line.

### Scheduled Purge Time

If you’ve added URIs to the schedule purge box above, set the time you’d like the purge to run here.

### Purge All Hooks

LiteSpeed recommends you Purge All when the hooks listed by default are run. If you have your own custom hooks that may affect the frontend of your website you can list these here as well. If not, just leave as is.

 

### [4] Excludes

 

This is where you can exclude specific pages, query strings, user agents, categories, and more from your website’s cache.

If you have custom checkout pages or forms where caching can break them (or whatever the case may be), you can easily exclude them inside this tab.

The settings are self-explanatory – add what you need to exclude in the relevant boxes (1 per line), and hit Save when you’re done.

 

### [5] ESI

 

 

### IMPORTANT

OpenLiteSpeed doesn't natively support ESI functionality. To make use of this feature on your OLS hosted websites you will need to use the QUIC.cloud CDN.

As it’s not natively supported by OLS, it is beyond the scope of this article.

Also, this is an advanced feature that requires that your WordPress theme is built correctly to work with it. It’s not as simple as configuring the plugin only, and even on LiteSpeed Enterprise you still need a compatible, properly configured/coded theme.

ESI isn’t necessary for 99.9% of websites.

You can learn more about ESI and the LS Cache plugin on the LiteSpeed documentation here:

https://docs.litespeedtech.com/lscache/lscwp/cache/#esi-tab

 

### [6] Object

 

Redis object caching can be configured directly within the plugin itself once turned on inside your GridPane account.

Object caching can provide a myriad of performance benefits by caching database queries so that MySQL doesn’t need to be called to process the same requests over and over again.

For example, when a user requests a WordPress page for the first time, a MySQL query is performed on the server. Redis caches this query, so when another user requests the same WordPress page, the results are provided from Redis without the need to query the database again.

We recommend you turn it ON. The correct settings (also detailed below) will be pre-configured.

### Enable Cache

As mentioned earlier, toggling this on within the dashboard will automatically turn the Enable Cache setting to ON.

### Method

Redis will be preselected. Don’t change this setting.

### Host

The host is autoconfigured by us: “/var/run/redis/redis-object.sock”

### Port

The port for Redis is “0”.

### Default Object Lifetime

The default setting is 360 seconds, which is 6 minutes. Keeping the time short will help prevent delivering STALE results, but if your website’s content doesn’t regularly change (you don’t have any dynamic content), you can increase this to a much higher TTL.

### Username

Not required.

### Password

Not required.

### Redis Database ID

“0”.

### Global Groups

The defaults here are good for most websites. Add your own if you have a specific use case.

### Do Not Cache Groups

Same as above – leave as is or edit/add your own if you have a use case.

### Persistent Connection

Leave ON.

### Cache Wp-Admin

This is fine left ON for most websites. Object caching has been known to cache the updates page, so if you see that the updates you’ve just made are still showing as available, this is probably why (it happens on Nginx sometimes too). If you see similar things in the backend and it’s causing you issues, you can turn this OFF.

### Store Transients

Leave this ON.

 

### [7] Browser

 

 

### IMPORTANT

This tab has a notice for OpenLiteSpeed users on setting custom headers. The necessary headers are all preconfigured on your GridPane OLS servers so you can ignore this message box.

Browser caching tells the browser to store things like images, CSS, and fonts.

This means that once downloaded, these files are loaded directly from the user’s device instead of repeatedly downloading them from the server every time they navigate between pages.

### Browser Cache

We recommend ON.

### Browser TTL

A TTL can be anywhere between 1 week (604800) and 1 month should work well for most sites. If changing from the default you will also need to edit your headers. Learn more here:

How to add your own custom headers on OpenLiteSpeed (or reset existing headers)

 

### [8] Advanced

 

Here you’ll find a couple of extra settings that can typically be ignored for most websites.

### Login Cookie

This setting can be ignored on GridPane.

### Improve HTTP/HTTPS Compatibility

Leave this OFF.

### Instant Click

We typically recommend reducing unnecessary server load by leaving this OFF.

It’s certainly an interesting option though and feels free to use it if you think it will help your visitor’s browsing experience on specific websites.

 

## Part 2. General Settings

General settings is where you can configure a few basics for your site, including getting started with QUIC.cloud. Here you can get your domain key and set your server IP – you’ll need a domain key if you want to make use of any QUIC.cloud services, such as their CDN and image optimization.

### Domain Key

You can request a domain key – which you’ll need if you’re looking to connect your website to QUIC.cloud.

The plugin mentions that their IP addresses may need whitelisting, however, this has not proved to be necessary thus far, and typically you’ll get your domain key in a minute or less (but be patient as it can take up to 15 minutes).

### Server IP

“Enter this site’s IP address to allow cloud services to directly call the server IP instead of domain name. This eliminates the overhead of DNS and CDN lookups.”

Learn more in the official documentation here:

https://docs.litespeedtech.com/lscache/lscwp/general/

 

## Part 3. CDN

The LiteSpeed Cache plugin can be configured to work with a CDN, including Cloudflare and LiteSpeeds own CDN QUIC.cloud (more info below).

To use a CDN with the LiteSpeed Cache plugin, please see the official documentation from LiteSpeed here:

https://docs.litespeedtech.com/lscache/lscwp/cdn/

 

## QUIC.cloud

You have the option to connect your website to QUIC.cloud, which is LiteSpeeds own CDN product built specifically for WordPress. It bills itself as “the only CDN service that can accurately cache dynamic pages (pages that can change frequently)”.

Along with the CDN, additional features also include image optimization, CDN-level reCAPTCHA, brute force protection, and critical CSS generation.

QUIC.cloud integrates directly with the LSCache plugin, and there’s a free tier available.

It’s an interesting offering, and you can learn more about pricing and sign up directly on their website here:

https://quic.cloud/cost/

And you can learn more about the service itself and how it integrates with LiteSpeed here on in the official LiteSpeed documentation:

https://docs.litespeedtech.com/products/lscdn/

 

## Part 4. Image Optimization

The LiteSpeed Cache plugin has an image optimization feature built-in that you could use to replace other plugins such as Shortpixel, Smush, EWWW, etc. This includes the creation of WebP images.

It requires a domain key which you can configure in the plugins General Settings. Learn more here in the official documentation here:

https://docs.litespeedtech.com/lscache/lscwp/imageopt/

 

## Part 5. Page Optimization

The LSCache plugin could also potentially replace any optimization plugins that you usually use. It includes the ability to:

You can learn more in the official documentation here:

https://docs.litespeedtech.com/lscache/lscwp/pageopt/

Some experimentation against your current preferred minification/optimization plugin may be a good idea to see which offers the best results (if applicable).

 

## Part 6. Database Management

Another handy tool in this plugins toolbox is database optimization, making additional plugins for this task unnecessary.

While this is useful, you should always approach database optimization with caution.

 

 

### IMPORTANT

ALWAYS backup your website before making database changes.

### [1] Manage

 

### Clean All

Press this button to run all database optimizations once. Use with caution so you don’t accidentally clean up data that you need.

### Post Revisions

This option will remove all post revisions from the database.  This means that you won’t be able to restore a page to an earlier saved version.

### Auto Drafts

If you have any unpublished page edits in progress you may want to skip this option.

If you know that there’s nothing that’s being worked on and/or that worked on pages are saved correctly as drafts, then you can safely run this option.

### Trashed Posts

Use this option to permanently delete any posts or pages that have been marked as trash, but not yet deleted.

### Spam Comments

This option permanently deletes any comments that have been marked as spam or trashed.

### Trackbacks & Pingbacks

Ideally, just disable these inside your Settings page, but use this option to delete any that already exist.

### Expired Transients

Transients are the result of a form of caching that can happen in the WordPress database with the results of remote API calls. This option clears all of the expired transients from the database.

### All Transients

This option clears ALL existing transients in the database.

After running this you may still find that you have a red X on this option. This is normal as some transients are regenerated on each page load.

 

## Database Table Engine Converter

This is another great option to both see if you have any MyISAM tables, and if they exist, convert them to InnoDB.

We recommend converting MyISAM to InnoDB.

A lot of the time when we see a performance-related issue on a website it’s related to the database not being optimized.

MyISAM is often a primary culprit and is an older, less efficient, and less reliable database storage engine than the more modern InnoDB.

Part of the reason for this is that MyISAM will lock whole database tables, which can have a logjam effect on database queries, whereas InnoDB only has row-level locking which allows queries to process much faster. Converting can result in huge improvements in response time and reduced server load.

By default, GridPane uses InnoDB, but older websites sometimes use MyISAM, and sometimes websites will have a mix of both. If you’ve migrated a website from elsewhere into GridPane, you may find that they contain MyISAM tables.

 

### [2] DB Optimization Settings

 

We recommend leaving these settings inactive for most websites and instead manually cleaning things up after taking a backup.

 

## Part 7. Crawler (Preload / Cache Warming / Cache Refresh)

The LSCache plugin has a crawler built-in that can be used ensure that your websites are fully cached for ensuring that your website’s cache is primed and up-to-date.

There is nothing required on your end for the server level configuration which is ready to go out-of-the-box on GridPane OLS.

You can learn more in the official documentation here:

https://docs.litespeedtech.com/lscache/lscwp/crawler/

 

### [1] Summary / [2] Map / [3] Blocklist

 

Each of these tabs will let you know the status of your cached pages across your website.

On the summary page the key is as follows:

The map tab displays the URIs currently in the crawler map.

The blocklist shows pages that couldn’t be cached. You can clear this list to attempt caching again.

 

### [4] General settings

 

 

### Important - Crawler Performance Issues / 503 Errors

OpenLiteSpeed doesn't have separate cache directories for all sites, instead, it shares a single directory to keep hashed versions for all the caches. High crawl settings for any large site on a server could cause a cache clash for all sites as the cache is managed at a single place by OLS.

For servers where you have any large sites or many sites on the same server, we recommend using a slower crawl limit for all sites so that each site can have a reasonable chunk of CPU time to create a cache. 

Do NOT use the crawler if you have a 1 CPU server that regularly goes above 25% hourly CPU usage.

If you’re experiencing performance issues due to the crawler, below offers some tips on alleviating the stress high crawl limits can impose. Settings will also vary depending on how large your server is.

### Crawler

If you want to set the crawler active, turn it ON.

Do NOT use the crawler if you have a 1 CPU server that regularly goes above 25% hourly CPU usage.

### Delay

The default is 500 microseconds (or 0.0005 seconds) which is fine in many cases. As noted in the infobox above, we recommend using a slower crawl rate for large sites and/or on servers where you have a high number of sites.

### Run Duration

This is the duration a crawl will run for at anyone time. 400 seconds is a fairly long time. Reduce across all your sites if you have large sites with many pages or many sites across the server.

### Interval Between Runs

The default 600 seconds should be fine for most cases. This is the wait time between runs.

### Crawl Interval

The best time will depend on the size of your site. Generally, once cached you likely won’t need regular crawls for most sites. Leaving the default of 3.5 days (302400 seconds) should be fine for most, but you could extend it to one week on sites that have many static websites.

### Threads

This is the number of active crawler processes that can be active at any one time. Setting to 1 may help reduce performance issues, but this depends on the type/number of sites and how many CPUs you have available.

If you have an active guest mode then this will have its own crawler.

On a 2 CPU server use 1 thread alongside a crawl interval that allows enough time for all sites to be crawled one by one.

### Timeout

The default of 30 seconds should be fine for most cases.

### Server Load Limit

The default of 1 should be fine for most use cases. If you have a large server with few sites you can test increasing this limit.

If the crawler reaches this limit it will be terminated to prevent performance issues.

Each running process that consumes CPU adds “1” to the server load. Do not increase past 1 on 1 CPU servers.

 

### [5] Simulation Settings

 

If you want the crawler to do something other than simulate a non-logged-in user when pre-caching your site you can set this up in this tab.

Learn more here:

https://docs.litespeedtech.com/lscache/lscwp/crawler/#simulation-settings-tab

 

### [6] Sitemap Settings

 

For the crawler to work, be sure to add your sitemap to this tab. The crawler will use your XML sitemap or sitemap index to crawl through your pages and pre-cache them.

You’ll be able to find this inside your SEO plugin setting if you’re using one. The default is /wp-sitemap.xml if you’re not using an SEO plugin. We generally recommend a custom sitemap or SEO plugin generated sitemap for best results.

 

## Part 9. Toolbox

The toolbox is a collection of tools to help manage your cache and website. It includes:

Below we’ll take a quick look at the various purge options. For the rest, please see the official documentation here:

https://docs.litespeedtech.com/lscache/lscwp/toolbox/

 

### [1] Purge

 

The settings here are mostly self-explanatory. They include:

You can also get very specific and purge based on:

You can learn more in the official documentation here:

https://docs.litespeedtech.com/lscache/lscwp/toolbox/#purge-tab

 

## Confirming Whether a Page is Cached or Not

Checking the website’s response headers for a HIT and MISS response is a quick and easy way to see whether or not a page is cached. To learn how to do this, please see the first part of our Diagnosing Caching Issues article:

Diagnosing Caching Issues

Or, alternatively, check out (and bookmark) this website by Hubert Nguyen (who’s also a member of the GridPane community):

https://test.ismypagecached.com/

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

