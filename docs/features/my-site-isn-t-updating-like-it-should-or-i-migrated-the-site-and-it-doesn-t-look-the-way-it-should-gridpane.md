# My site isn’t updating like it should or I migrated the site and it doesn’t look the way it should? | GridPane

# My site isn’t updating like it should or I migrated the site and it doesn’t look the way it should?

 

2 min read 

## Introduction

This short troubleshooting article covers the primary issues that can occur when migrating a website to GridPane, and the most likely reason that you may be having an issue updating a specific website.								

 

### Information

If you've recently migrated a website and the following has not helped you pinpoint the root cause of your issue, please check out our full article on diagnosing migration issues here.

## Top 3 Migration Issues

If you update your site and you see that the site looks the way it should while logged in but doesn’t look right when you’re logged out, typically, it’s due to one of the following three reasons:

Hosts always tend to have their own quirks, so once you know what they are, it’s usually smooth sailing after that.

## Layered Caches

You’ve migrated your website in but it looks broken it may be due to layered caches. This can occur if you visit your website before the migration is complete, as it could cache the partially created website. This can result in a layered cache, essentially breaking your website on the front end.

To fix this, clear your website’s cache via the website customizer caching tab:

You can also do this inside of your GridPane account using the Self Help tools as shown in the image below:

## GridPane Caching Plugins Have Been Deleted

If you or your client has deleted the caching plugins (Redis Object Caching and Nginx Helper on Nginx, or the LiteSpeed Cache plugin on OpenLiteSpeed), but caching is still active at the server level, this could potentially cause issues with WordPress functionality.

You can reinstall these plugins by toggling caching OFF and then back ON again.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

