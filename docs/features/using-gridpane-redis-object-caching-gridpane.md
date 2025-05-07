# Using GridPane Redis Object Caching | GridPane

# Using GridPane Redis Object Caching

 

3 min read 

 

### INFO

This article gives an overview of Redis Object Caching and how to use with Nginx.

### Table of Contents

 

## Introduction

Redis is an open-source (BSD licensed) key-value store that can operate as both an in-memory store and as cache. A data structure server in its own right, it can be easily paired with a relational database like MySQL to speed things up by caching database queries.

WordPress uses a MySQL database to cache internal application objects (breadcrumbs, menu items, etc.), which is generally an expensive process. Since the database also handles queries for page requests, this can contribute to one of the most common bottlenecks in WordPress, often causing increased load times.

When a user requests a WordPress page for the first time, a MySQL query is performed on the server. Redis caches this query, so when another user requests the same WordPress page, the results are provided from Redis without the need to query the database again.

If the query is not cached in Redis, the results are provided by MySQL, which is then added to the Redis cache. If a particular value is updated in the database, the corresponding Redis value is invalidated to prevent bad cache data from being served to the user.

All GridPane WordPress sites come deployed with all the server-side wp-config.php configurations required to use the Redis Object Caching for WordPress and the necessary plugin already installed. To be able to use this caching is simply a matter of activating a plugin and enabling the caching.

 

## Step 1. Activate GridPane Redis Object Caching in the UI

Head over to the Sites page inside your GridPane account and click on the website you wish to activate object caching for to open up the website customizer:

Click through to the Caching tab, and then click through to Object Caching. Here you simply need to toggle it on.

 

## Step 2. Enable Redis Object Caching

Activating Redis Object caching within the UI will automatically install the Redis Object Cache plugin.

You can view this directly on the plugins page, and here you can also click through to the settings page:

Now Redis Object caching needs to be enabled. Click through to the plugin settings page either via the plugins page as shown in the image above, or via the WordPress admin bar > Object Cache > Settings.

On this settings page, you can enable Redis Object caching here:

Click the Enable Object Cache button.

In the Overview tab, the Status will change to Connected, and object caching will be enabled.

 

## Step 3. Flush the Redis Object Cache

### Flush the Cache Within GridPane

You can flush the Redis Object cache directly inside your website customizer (or ALL websites caches – page, object, opcode) here:

### Flush the Cache Within WordPress

Inside your WordPress dashboard you can clear the cache via the admin bar > Object Cache > Flush Cache:

Or directly within the plugin settings page via the Flush Cache button:

You will receive a dismissible notification, at the top of the settings page under the Plugin title, that the cache has been flushed.

 

## Disabling Redis Object Caching

You can easily disable object caching for your website:

 

## What if I Delete the Redis Object Cache Plugin?

If you delete the object cache plugin, then all external Redis-based object caching is disconnected. WordPress does have its own internal PHP-based object caching using the database and transients; however, this can be flushed using the GridPane Tools to clear the cache.

The Redis Object Cache plugin is installed by default on all site builds, but if you happen to delete it, simply toggle Object caching OFF and then back ON again, and it will be reinstalled for you.

 

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

