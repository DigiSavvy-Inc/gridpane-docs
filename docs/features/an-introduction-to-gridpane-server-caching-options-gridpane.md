# An Introduction to GridPane Server Caching Options | GridPane

# An Introduction to GridPane Server Caching Options

 

5 min read 

## Introduction

If you’re new to GridPane, our server caching options may be a little confusing at first, especially if it’s your first time venturing outside of the more traditional caching plugins such as WP Rocket, Swift Performance, W3TC, etc.

Some of these perform admirably well – especially Rocket and Swift – but they simply can’t perform as well as what our native server caching can offer.

### Table of Contents

 

 

### Nginx vs OpenLiteSpeed/LiteSpeed

There's a lot of misinformation about how well LiteSpeed/OpenLiteSpeed performs in comparison to Nginx. The truth of the matter is that from a pure performance standpoint, there's very little difference between the two when configured correctly. This should not be the main consideration when choosing between the two - and if it was, we'd likely recommend Nginx.

## Page Caching and Object Caching

GridPane offers two types of caching: Page caching (2 options available) and object caching.

Our page caching options will cache your individual page assets. Once a page is loaded it creates a static version of it, which can be loaded much faster the next time someone visits that page.

Object caching caches database queries (including things like menu items, breadcrumbs, post author names, dynamically generated archives like blog roll pages, etc), which means the database doesn’t need to perform the same queries each time the page is loaded.

 

## GridPane Nginx Page Caching Options

no plugin-based solution will ever match the performance of Nginx server-based static asset and page caching.

### FastCGI Caching

FastCGI is perfect for websites with high concurrent traffic (where it has an edge over Redis Nginx Page caching), and it’s also ideal for websites where content regularly changes. For example, popular blogs and news websites that regularly publish new content and/or have active comments or forums with publically accessible content.

In these cases, micro-caching is perfect as it will update the cache in the background each time a visitor loads a page, ensuring that all future visitors are served with the latest content.

For most other use cases where your site traffic isn’t thousands of concurrent visitors hitting your website at the same time, and your content is fairly static, Redis Nginx Page Caching may be a better fit and is what we recommend for most websites.

### Redis Nginx Page Caching

Not to be confused with the Redis Object cache, Redis Nginx page caching is another highly performant page caching solution that you can take advantage of on GridPane Nginx servers.

Most of the websites on GridPane use this option and we generally recommend it for most websites.

If you’re not experiencing thousands of concurrent visitors hitting your website at the same time, and your content is fairly static, Redis Nginx Page Caching is usually the best option, and this includes both brochure-style websites as well as WooCommerce, LMS, and membership sites.

Redis is extremely performant into high levels of concurrent visitors, and it will also auto-purge itself more effectively than FastCGI, which can sometimes use a significant amount of RAM on very large websites, and/or on servers where you have many websites hosted and all utilizing it.

 

## OpenLiteSpeed Page Caching

OpenLiteSpeed uses the excellent caching system created by the LiteSpeed team. This is managed via the LiteSpeed cache WordPress plugin which integrates directly with the server-level page and object cache (more on object caching in the next section below).

The LiteSpeed Cache plugin is one of the major reasons that both OpenLiteSpeed (OLS) and LiteSpeed Enterprise are so highly touted by the WordPress community. It is an exceptionally well-built caching system and with GridPane OLS you can take advantage of this for the websites that you host.

Like our Nginx page caching, the LiteSpeed cache will perform exceptionally well, and it can be configured for any type of website – whether dynamic or static in nature.

 

## Redis Object Caching

Redis is an open-source, in-memory data structure store. For WordPress purposes, it can be used alongside a MySQL database to cache your database queries, and dramatically reduce the number of requests that reach your database, thereby decreasing the amount of work your server needs to do in order to serve up your website’s pages.

When a visitor hits a page on your website that hasn’t been cached, MySQL will serve up the information needed, and this will then be cached by Redis so these same queries don’t need to go through MySQL the next time around. When the next visitor comes along, Redis will instead serve the information instead of MySQL.

Reducing the amount of work your server has to do means your website/s will load faster and be able to handle more traffic.

On Nginx, this is managed via the Redis Object Caching plugin.

On OpenLiteSpeed, this is managed via the LS Cache plugin.

 

## OPcache

OPcache provides an improvement to PHP performance by storing precompiled script bytecode in shared memory, thereby removing the need for PHP to load and parse scripts on each request.

On Nginx, this can only be cleared inside the UI or via CLI along with the other cache types, but it also has a very short TTL so manually clearing it is generally never necessary. Learn more here:Configure PHP: Configure PHP OPcache

On OpenLiteSpeed it can be managed via the LS Cache plugin. Learn more here:OpenLiteSpeed Caching and the LiteSpeed Cache Plugin: Caching Settings

 

## Getting Started with GridPane Server Caching

The following articles will help you get started using our server caching options. If you’re unsure where to start, we recommend checking out this article on caching strategy first:

Caching Strategy

And you can learn how to set up our different caching options here:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

