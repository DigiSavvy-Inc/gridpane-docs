# Using GridPane Nginx Redis Page Caching | GridPane

# Using GridPane Nginx Redis Page Caching

 

6 min read 

### Table of Contents

 

## Introduction

The GridPane Nginx Stack also features Redis page and static asset caching as a high speed and reliable in memory solution.

Most people know and use Redis as a highly efficient, powerfully configurable, and incredibly fast object cache for things such as Database queries, but it can also serve double duty as a static caching solution integrated with Nginx.

 

 

### Note

This article gives an overview of Redis Page Caching which is enabled via the toggle in the dashboard. The plugin Nginx Helper is used alongside it to enable easy purging.

## Redis Nginx Page Caching: Best Use Cases

GridPane comes with 2 Nginx caching systems. The other is FastCGI which employs microcaching.

Redis Nginx Page Caching is what we recommend for most websites.

If you’re not experiencing thousands of concurrent visitors hitting your website at the same time, and your content is fairly static, Redis Nginx Page Caching is usually the best option.

Redis is extremely performant into high levels of concurrent visitors, and it will also auto-purge itself more effectively than FastCGI, which can sometimes use a significant amount of RAM on very large websites.

There are, however, situations where FastCGI may be the better fit.

### The Case for FastCGI

FastCGI Caching is perfect for websites with high concurrent traffic (where it has an edge over Redis Nginx Page caching), and it’s also ideal for websites where content regularly changes. For example, popular blogs and news websites that regularly publish new content and/or have active comments, or forums with publically accessible content.

In these cases, microcaching is perfect as it will update the cache in the background each time a visitor loads a page, ensuring that all future visitors are served with the latest content.

 

## 1. Enable Nginx Redis Page Caching

You can enable Redis Nginx Page caching and change the cache TTL inside your website’s customizer.

### Enabling Redis Nginx Page Caching

To get started, head over to the Sites page inside your account and click on the website you want to activate caching for to open the Site Customizer:

Click through to the Caching Tab, and then click Redis Caching Toggle:

Your site will now have Nginx Redis Caching enabled with GridPane custom configurations.

### Adjust Cache Time To Live (TTL)

Time to live (TTL) is the time that your page is stored in a caching system before it’s deleted or refreshed.

The default setting for Redis Nginx Page caching is 30 days (2592000 seconds).

In most cases, 30 days is a good number of days for your cache. However, if you need to change it, you can adjust the TTL inside the Page Cache TTL (seconds) box, and then click Update:

An example use case for this may be that you have a form that requires WordPress nonce validation.

### Confirm Your Caching is Active

If you want to confirm your caching is now active you can visit your site and check the response headers using the site inspector you will see that caching has been enabled.

Part 3 of this article below covers this in more detail.

 

## 2. Enable Redis Cache Purging

Nginx cache purging is one of the premium features of the Nginx Plus platform but, as is usual with the open-source community, a resourceful community member has stepped into the gap and provided an invaluable asset to enable cache purging on the FOSS version of Nginx.

The GridPane stack is custom compiled with the redis-nginx, redis2-nginx, and srcache-nginx-module, which allow for a Redis server to be used as a static cache, and enable cache purging when content updates.

To enable cache purging we have installed and activated the Nginx Helper plugin.

This plugin allows for the incremental purging of your site’s cache when you update content, such as posts, pages, comments etc.  The plugin has been installed, but you need to configure it to suit your specific purge requirements.

You can find it under Settings Nginx Helper

You will need to check Enable Purge and select Redis cache as the Caching Method.

Under Redis Settings, make sure Hostname is set to 127.0.0.1 with a Port of 6379, and Prefix is set to nginx-cache: (the trailing colon is required).

Under Purging Conditions, you should select what content you would like to trigger the purging and updating of the cache.

Click Save All Changes when you have configured the options to suit your needs and now the cache will automatically purge outdated content as you update your GridPane site content.

### What if I delete the Nginx Helper Plugin?

If you delete the Nginx Helper plugin, then the server will have difficulty clearing the cache on content updates, instead, you will need to use the GridPane Tools to clear the cache.

You can always download and re-install the Nginx Helper plugin from the WordPress Org Repository at any time, this can be done directly from the plugins interface in wp-admin.

 

 

### Important

If you switch from FastCGI to Redis Page caching or vice versa, make sure you also switch the caching method inside Nginx Helper plugin inside your website.

## 3. How to check if a page has been cached

First, open up your website in an incognito window. Next, right click and choose “Inspect“, select the “Network” tab, and then reload the page. The result will look similar to the image below.

Click on your URL on the left hand side to open up the box on the right, then down until you see the “Response Headers” section. If our caching is active you’ll see the following for Redis Nginx Caching:

```
X-Grid-SRCache-Fetch
```

If caching is turned on, you’ll see X-Grid-SRCache-Fetch with a value of either:

```
HIT | MISS | BYPASS
```

HIT means the website is cached.

MISS means this page hadn’t been cached yet as it’s the first time it’s been visited since either the cache has been activated or cleared -on reload it should say HIT.

BYPASS means this page has been excluded and will never be cached.

Here is what Redis Nginx Page caching looks like when turned on (on activating I got a value of MISS, but now the page has loaded, on reload I have a value of HIT as shown below):

In the above image you can also see X-Grid-SRCache-TTL: 2592000.

TTL stands for time to live, and this tells your browser how long it should cache this page for. The number next to it is the time in seconds. 2592000 converted into days = 30. This is the default value for Redis Page caching, and X-Grid-SRCache-TTL: 2592000 tells your browser to cache this page for 30 days.

### Caching won’t take place while you are logged in

When logged into your website you will see that the cache is bypassed, and in your dashboard you will see:

```
cache-control: private, no-store
```

This forces browsers and CDNs never to cache.

 

## Nginx Cache Exclusions

By default we exclude certain common pages that should never be cached. You can learn more about what we exclude and how to make further exclusions in the following articles:

 

## GP-CLI

While we recommend using the toggles inside your GridPane account to configure your caching settings, we have GP-CLI available. Click the link below to see our caching-related GP-CLI commands:

GP-CLI Quick Reference: Caching

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

