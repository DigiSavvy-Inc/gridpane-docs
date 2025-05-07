# How to Clear Your Website Caches (All Methods) | GridPane

# How to Clear Your Website Caches (All Methods)

 

4 min read 

## Introduction

At GridPane there are 3 different caches that apply to your websites. These are:

This article will cover the different methods available to you for clearing them.

To learn more about each caching type this article offers an introduction along with links for further reading: An Introduction to GridPane Server Caching Options

### Table of Contents

 

## Clearing the Cache: Best Practices

Generally, when clearing your website caches you will ideally clear the page of specific pages on an as-needed basis instead of clearing the entire website’s page cache.

The Redis Object cache and OPcache will generally take care of themselves.

However, clearing the entire cache is often useful when your troubleshooting or making significant changes to your websites. Also, if you have plugins such as pagebuilders installed, these may often make sweeping CSS changes that affect the entire website.

In these cases, it’s best to clear the entire cache to ensure that your website displays correctly on the frontend.

 

## Clearing Caches on Nginx within WordPress

The Nginx page cache is managed via the Nginx Helper plugin. The Redis Object Cache is managed via the Redis Object Cache plugin. The OPcache can only be cleared via your GridPane dashboard or CLI.

Both the page and object cache plugins are automatically installed on your websites when you create them. Nginx Helper works for both Redis Page Caching and FastCGI caching – just make sure that you set this correctly directly within your website.

### Clearing the Nginx Page Cache

You can clear the entire page cache inside your Dashboard > Settings > Nginx Helper:

You can also set purging conditions using the options on this settings page.

You can clear individual pages directly on the frontend of your website by navigating to the page you wish to clear and using the Purge Cache option in the WordPress admin bar:

### Clearing the Object Cache

You can clear the object cache either inside Dashboard > Settings > Redis Object Caching:

Or via the option in the WordPress admin bar on the frontend of your site if you’ve checked the setting inside the plugin settings:

 

## Clearing Caches on OpenLiteSpeed within WordPress

The page, object, and opcache can all be cleared directly within the LiteSpeed Cache Toolbox section. Pages can be cleared individually on the frontend of the website along with various other purging options.

### Clear via the Website Backend

The settings here are mostly self-explanatory. They include:

You can also get very specific and purge based on:

### Clear via the Frontend

On the frontend you also have numerous options for clearing your website’s different caches. This includes purging individual pages, clearing the entire page cache, clearing the entire object cache, clearing the entire opcache,  and clearing ALL caches.

### Further Reading

You can learn more in our OpenLiteSpeed caching guide and/or the official documentation here:

 

## Clearing Website Caches via the GridPane Dashboard

You can clear all your caches inside of your GridPane account.

### Clear Nginx Caches via the Website Customizer

On Nginx, the easiest way is inside your websites customizer, in the caching tab where you can either clear the page or object cache, or both:

### Clear Nginx or OpenLiteSpeed Caches via Tools

You can also do this inside of your GridPane account using the Self Help tools as shown in the image below:

 

## Clearing Caches via CLI

Clearing your caches via CLI is quick and easy. You’ll need to connect to your servers first, but then it’s just a case of copying and pasting a command.

If this is your first time connecting to your servers, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Clearing Individual Website Caches via CLI

To clear the caches of an individual website, run the following command (replacing site.url with your website’s URL):

```
gp fix cached site.url
```

For example:

```
gp fix cached mywebsite.com
```

 

### Clearing ALL Website Caches via CLI

To clear the caches of all the websites on your server, run the following command:

```
gp fix cached
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

