# Using a CDN With GridPane | GridPane

# Using a CDN With GridPane

 

6 min read 

## Introduction

We’re sometimes asked about CDNs and whether or not they should be used, and which we recommend, etc. In this article, we’ll offer some guidance and recommendations, along with some additional info that is generally useful to be aware of when using a CDN.

### Table of Contents

If you have further questions that aren’t answered in the sections below, please post them in the community forum, and we can look at getting these documented once answered.

 

## Part 1. Do You Need a CDN?

The vast majority of websites don’t need and likely won’t benefit from using a CDN. In fact, using one can on occasion slow things down.

The three main benefits of a CDN are as follows:

At GridPane you have access to both server-level page and object caching so your performance is going to excellent right out of the gate, and as your buying your servers directly from your IaaS provider, you’ll have a huge amount of bandwidth available.

Generally, if you still wanted to use one for your sites, Cloudflare’s free plan is a great choice, which then offers additional security at no cost. More on this

 

## Part 2. When to Use a CDN

There are 2 specific scenarios where a CDN can make a lot of sense and are worth the investment. However, this doesn’t necessarily mean you need one, and Cloudflare free will often suffice.

### Scenario 1: Your Visitors Are From Different Regions or Countries

CDNs generally become useful when you’re visitors are coming from multiple countries, or multiple regions/states if you live in a large country. By serving your website from a datacenter that is closer to their location, you can cut down your website’s TTFB and response times.

### Scenario 2. You Have a Very High Traffic Website

When you have a website that receives a huge amount of traffic, a CDN will reduce the load off of your server, serving your website content to your visitors directly without your GridPane server needing to be involved. This means you can serve more concurrent visitors without needing to increase your server’s CPU count.

 

## Part 3. CDNs and Caching, Routing, and Response Headers

While there’s nothing special needed for a CDN to work with your GridPane websites, the following information should prove useful.

### Page Caching

A CDN will replace the need for server-level caching. Its function is the equivalent of our page caching, and just like you shouldn’t use our caching and a regular caching plugin together, you shouldn’t activate our page caching when using a CDN. Doing so will likely just result in strange issues due to the caches overlapping one another.

Keep our page caching inactive, and don’t use other caching plugins in addition to your CDN.

### Object Caching

Object caching can and should still be used. It will assist in speeding up database queries whenever requests BYPASS or MISS the page cache, and is particularly useful for dynamic websites.

### Root/WWW Routing

You should have no issues with the way your routing is configured when using a CDN. We’ve already taken this into account in an update to prevent issues that occur when using Cloudflare APO, which doesn’t work correctly when a server routing is properly configured. It instead assumes that the server isn’t going to be properly configured, which we solved for out of the box by loosening our strict control on these constants.

You can learn more here:Manage Site Domains and Site Routing (non www vs www): Background Info

### Response Headers

When inside your websites admin area, we set the following response header so that your website’s cache is  automatically bypassed:

```
cache-control: private, no-store
```

This forces browsers and CDNs never to cache, so you should have no issues caused by caching when using a CDN with your GridPane websites, and you can confirm for yourself by checking the header like in the following screenshot, along with a BYPASS response:

We don’t set any other headers that should interfere, so if you happen to see one that is causing issues, it’s likely that another plugin within your website is setting this.

 

## Part 4. CDN Recommendations

While we have no hesitation in recommending the following CDN solutions, this doesn’t mean that others out there aren’t worth your consideration. These are just the most popular ones the GridPane communities tend to use, and they have an excellent service that’s very competitively priced.

Knowledge base articles will be published for setting up BunnyCDN and QUIC.cloud in the future.

### 1. Cloudflare FREE

Cloudflare’s free plan is straightforward to set up and includes numerous features alongside their CDN. It’s a fantastic service.

In fact, one of our clients competed in the 2022 Review Signal WordPress Hosting Benchmarks in the enterprise category and earned Top Tier honors using a GridPane provisioned server and Cloudflare’s free plan. Some of their websites serve 70 Terabytes of data per month via Cloudflare free. It’s truly impressive.

By default, Cloudflare’s free plan caches common static content file extensions, including JS, CSS, all common image extensions, webfonts, common document, and media extensions. The full list can be found here.

For a detailed look at using Cloudflare’s free CDN and caching with GridPane, check out this article: Cloudflare Caching and GridPane

### 2. Cloudflare APO

Cloudflare’s Automatic Platform Optimization (APO) for WordPress offering is excellent. They have a WordPress plugin, it’s easy to set up, and it starts from $5/month. They’re a popular choice, and you check out our article on setting up APO for your sites here:How to Set Up Cloudflare APO

As a side note, Cloudflare’s plugin doesn’t have as good a rating as you might expect, however, after reading through the negative reviews, I suspect the issues were less to do with Cloudflare and more to do with the website owner not understanding how to set things up correctly.

### 3. QUIC.cloud (OpenLiteSpeed Only)

QUIC.cloud is LiteSpeed’s own CDN product built specifically for WordPress. It bills itself as “the only CDN service that can accurately cache dynamic pages (pages that can change frequently).”

Along with the CDN, additional features also include image optimization, CDN-level reCAPTCHA, brute force protection, and critical CSS generation.

QUIC.cloud integrates directly with the LSCache plugin, and there’s a free tier available.

It’s an interesting offering, and you can learn more about pricing and sign up directly on their website here: https://quic.cloud/cost/

### 4. BunnyCDN

BunnyCDN is another popular CDN that has a dedicated WordPress plugin. It’s excellent value for money, and like Cloudflare, it’s easy to set up (if only caching static files like CSS, JS, and images remotely – full page caching isn’t simple) and offers a ton of features that can be customized – including DDoS protection.

It starts from as low as $1/month. Learn more here: How to Set Up Bunny CDN for WordPress

 

## Troubleshooting

Generally, if you experience an issue with a CDN it’s probably due to it not being set up correctly, another plugin is adding additional response headers that are causing issues, or it’s a common caching issue that can easily be resolved.

The troubleshooting steps are largely the same as detailed in our diagnosing caching issues article:Diagnosing Caching Issues

However, you may also want to first deactivate the CDN and check if your issue is resolved. If so, clear the CDN cache and retest.

You may also want to check if disabling all plugins temporarily solves the issue as well, as it’s possible one of them could be causing conflicts or setting cache-specific response headers.

If you’re unable to diagnose the cause, the CDNs support desk is usually the best place to seek advice. You can also post in the community forum as well.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

