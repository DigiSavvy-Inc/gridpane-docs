# GridPane Database Rewrites and Workflow | GridPane

# GridPane Database Rewrites and Workflow

 

5 min read 

## Introduction

In this article, we’ll take a look at how and when GridPane will run database rewrites on your servers, as well as how to run these operations in the most efficient way possible to improve your workflow and reduce the time it takes to run these search and replaces.

### Table of Contents

 

## GridPane Search and Replaces

GridPane offers 2 options for search and replaces (also commonly referred to as database rewrites):

Our implementation of Interconnect/IT is extremely thorough and does an excellent and reliable job of replacing ALL necessary URLs during operations that require it.

In our earlier days, we only used to use WP-CLI, but this can sometimes be unreliable and miss URLs during staging pushes.

Over time, we have refactored our search and replace functionality, and depending on the operation running, it is now 10-20 times faster than our earlier versions. That said, on a very large database, this can still take a long time to run.

 

## When Database Rewrites Take Place

GridPane will rewrite the URLs in your databases when you run certain functions:

### Routing

When you run one of the above functions, our search and replace will automatically set your website’s routing correctly to match its current state. You can learn more about routing here:

Manage Site Domains and Site Routing (non www vs www)

### HTTP <-> HTTPS

When you toggle SSL ON or OFF, our system will automatically configure your website to be served over HTTP when your website has no SSL and over HTTPS when you activate an SSL.

You do not need to force SSL to always be on using a plugin or any kind of Nginx rule. In fact, if you did force HTTPS via your own custom Nginx rule, you may prevent Let’s Encrypt from being able to renew or provision an SSL for your website.

Forced HTTP > HTTPS in the Nginx main-context.conf include

Also, when you activate or deactivate an SSL, the system is rewriting the home and siteurl in your wp_options table before it ever gets to search and replace. The flow is as follows: –

At this point, your SSL will be live on your website, and the HTTPS version will load. The remaining rewrites will then take place in the background.

### Email Addresses

If your email address includes “staging”, for example, [email protected], we presume this is unintentional and when you push from Staging to Live we will rewrite it to the primary domain. So [email protected] would become [email protected].

When pushing from Live to Staging, however, our system does NOT replace email addresses this way.

During cloning or domain swaps, it’s possible that emails may be updated in cloning if it’s using the full domain name. This, however, will not replace emails from the database users table (user_email, username, etc) and would only replace it inside your website’s frontend content.

Our previous iteration strictly didn’t touch emails, however, that required a significantly more complex regex which was more time-consuming and resource intensive.

 

## Improving Your Workflow

To improve your workflow and decrease the time it takes to run staging, cloning, and domain swap operations, there is an optimal way to approach them. Our search and replace runs through rewrites intelligently as needed, and this includes the need for routing and rewrites to either HTTP or HTTPS, depending on whether an SSL is in the mix.

We’ll look at this below, and while it may not always be possible, these steps in the right order will help you reduce the time these rewrites take and the resources needed to run them when you are able to.

 

### Cloning to a new URL

When you clone a website to a new URL, the system will attempt to match the states of the origin website (caching, PHP settings, etc), including provisioning an SSL certificate.

If no SSL is active on the origin site, then you’re all set.

When cloning a HTTPS site, you can decrease the rewrite time by setting the DNS for the URL you’re cloning to live and making sure it’s resolving before you initiate the clone.

This ensures that the SSL won’t fail, and so the database won’t need rewriting from HTTPS to HTTP, because the system will just run a single compound regex.

If an SSL attempt does fail during cloning, the system will run additional rewrites to HTTP, which is [only] 3 patterns via regex. This is still fast but can make a difference on very large websites.

To summarise, if an SSL is provisioned, the system does just one rewrite, but if it fails, it will do 3.

 

### Staging and Domain Swaps

Like with cloning to a new URL, if both domains have an SSL certificate before the swap/push, the system doesn’t need to check for HTTP/HTTPS URLs and use a simpler compound regex.

You can reduce the time by ensuring both the live and staging websites have an SSL certificate before the push begins and that the live and alias domain both have SSLs before the swap begins.

Also, for staging, ensure that the routing (none/root/www) on the staging website is the same as on the live site before you make the push.

 

### Migrating a website into GridPane

When you migrate a website into GridPane you may want to set the correct routing inside the website customizer in the domains tab before importing your website.

If you’re importing a website that already has an SSL, you may want to provision an SSL certificate in advance using one of our DNS API integrations so that the site imports into a provision an SSL beforehand:

If that’s not possible though, when the time comes to set the website live and provision an SSL, you can choose to NOT run any database rewrites if your URLs are already correctly set up for HTTPS:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

