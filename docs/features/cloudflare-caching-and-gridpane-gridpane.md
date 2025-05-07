# Cloudflare Caching and GridPane | GridPane

# Cloudflare Caching and GridPane

 

4 min read 

### Table of Contents

 

## Introduction

Cloudflare’s free tier is extremely popular within the GridPane community, and for good reason. One of the things we’re frequently asked about when using Cloudflare is “is it OK to use Cloudflare caching with GridPane caching?”.

The short answer is: YES.

We rarely see any kind of issues when running Cloudflare’s proxy and free tier level caching alongside our server caching. In this article, we’ll take a look at how to check if Cloudflare is enabled on your site, what it actually caches, and when you may need to clear the Cloudflare cache.

 

## Cloudflare’s Free Plugin

Cloudflare offers a WordPress plugin that can make managing your Cloudflare settings easier, as well as run a cache clear from within your website instead of your account. You can also utilise their excellent APO service with this plugin too.

The plugin is freely available in the WordPress plugin repository here:Cloudflare WordPress Plugin

 

## Cloudflare’s Free CDN Caching and GridPane

Cloudflare have their own dedicated article on this topic that you can read here (it’s old but still worth a read), and they have their own official documentation on working with their caching. You can check out both via these links:

### What Cloudflare Caches

Here are the highlights:

### What Cloudflare Does NOT Cache

### Cloudflare Page Rules

The free tier also comes with 3 page rules, which you could use to implement more comprehensive caching at Cloudflare.

Caching additional content at Cloudflare requires a Cache Everything Page Rule. Without creating a Cache Everything Page Rule, dynamic assets are never cached even if a public Cache-Control header is returned. When combined with an Edge Cache TTL > 0, Cache Everything removes cookies from the origin web server response.

You can learn more here:Create Edge Cache TTL page rules

If you do enable this, then you will need to be careful of using two layers of caching together. Unlike a DNS, server, and application firewall, which don’t conflict with one another, caching is the exact opposite, and using full page caching at both Cloudflare and the server level may interfere with one another.

You will also want to ensure that you don’t cache the /wp-admin area, and Cloudflare also caches XML responses when using Cache Everything.

 

## How to Check if Your Website is Being Served by Cloudflare

To check whether your website is being served by Cloudflare you can check the HTTP Response headers.

To do this, head over to your website and right-click and choose “Inspect“. This will open up the developer tools and from here you can click through to the network tab:

Refresh the page, and then click on the name of your website in the left-hand breakdown:

If your website is being served by Cloudflare, here you will see all of their various response headers, including their IP address, the cache status, and that the server is “Cloudflare”:

 

## How to Check the Caching Status of Your Website

Cloudflare adds the caching status to your website’s response headers so it’s easy to tell whether a resource is being cached at and served via Cloudflare.

Still in Developer tools (see the previous section), click on a resource on the left-hand side and you’ll be able to see that resource’s status.

### Example 1: Check Page Caching Status

For example, here I’m checking the page itself to see if it’s being cached:

The cache response is “DYNAMIC”, which is what I’m expecting with the default Cloudflare cache options.

DYNAMIC indicates: Cloudflare does not consider the asset eligible to cache and your Cloudflare settings do not explicitly instruct Cloudflare to cache the asset. Instead, the asset was requested from the origin web server.

Here we can also see that GridPane server-level caching is active and that the page is being served from the LiteSpeed cache:

### Example 2: Check Style.css caching status

Again on the left-hand side, we can see all the various resources that have been loaded. If we select the style.css file, we can see that this is being served as HIT by Cloudflare:

This means that the resource was found and served from Cloudflare’s cache.

 

## Purging the Cloudflare Cache

The easiest way to purge the cache is to install the WordPress plugin which allows you to manage a variety of different settings directly inside your website.

Alternatively, inside your Cloudflare account, click through to your website, and then select Caching and then Configuration. Here you can run a cache purge:

A little further down this same page, you can also enable Development Mode if you’re actively working on the website:

 

## Further Reading

You can learn more about caching strategy and GridPane in these articles:

And you can learn how to diagnose caching related issues here:

Diagnosing Caching Issues

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

