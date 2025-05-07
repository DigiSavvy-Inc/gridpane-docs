# PHP Workers and WordPress: A Guide for Better Performance | GridPane

# PHP Workers and WordPress: A Guide for Better Performance

 

31 min read 

PHP Workers are an important piece in the high-performance hosting puzzle. This guide will walk you through the fundamentals and offer some real-world guidelines for all the common use cases.

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1200'%20height='638'%20viewBox='0%200%201200%20638'%3E%3C/svg%3E)

### Table of Contents

 

## Introduction

Depending on your hosting experiences in the past, you may have come across the PHP Worker Tax. That conversation usually goes something like this (minus the sarcasm):

Oh, your website is slow and completely unreliable when you have a few people trying to checkout at the same time? You need more PHP workers! Upgrade to our 60 site plan, even though you only host 8 websites…

This is the PHP worker tax.

Most managed hosting companies have rigid, container based hosting plans that can be great for your average brochure style website, but for any dynamic website with lots of cache bypassing traffic, PHP worker restrictions on these types of plans can quickly become a costly pain point.

As you grow your own hosting business and host bigger and more complex websites, it’s important to have a fundamental understanding of what PHP workers are, and how they will affect your websites performance.

In this article we’ll look at:

We’ll be primarily focusing on Nginx and in the future, we’ll update this article with info on OpenLiteSpeed. If you’re using Apache, it may be time to consider not using Apache..

### Do You Actually Need to Care About PHP Workers?

If you only host low traffic, brochure style WordPress websites then technically no…

However, as a serious WordPress professional you should absolutely take the time to learn what PHP workers are all about. This will not only help you become a better developer, but it will also help you to become better at selling your own WordPress hosting / care plan services and demonstrating your expertise.

Part of what makes GridPane so powerful is that it gives serious WordPress professionals the tools to build their own enterprise capable hosting service / care plans. Understanding how PHP workers operate will help you: –

If you plan on growing a serious hosting business or even hosting a moderate to heavily-trafficked website that has dynamic content, knowing how to manage PHP workers is a valuable skill.

Let’s dive in!

 

## Part 1. PHP Worker Fundamentals

Let’s take a look at what they are, what they’re responsible for, and how this relates to hosting your WordPress websites.

### A Few Bite-Size Definitions

##### PHP Worker

A PHP worker is a background computing process responsible for processing PHP code.

##### Worker Pool

The worker pool is the pool of available PHP workers that are ready to take on requests from the web server (Nginx / OpenLiteSpeed).

##### PHP Threads

A thread is a small unit of instructions which can be executed by a processor (our server’s CPU).

### What are PHP workers?

A PHP worker is a PHP processor that handles requests allocated by the webserver (Nginx / OpenLitespeed) when these requests require PHP code to be processed. Once a request is completed, the PHP worker then returns the information back to the webserver.

They are responsible for generating the HTML pages that you and your visitors see when you visit your website, as well process background tasks such as WP-Cron or security plugin related work.

It’s the job of PHP workers to process any requests that “BYPASS” or “MISS” your website’s cache (learn more about caching here). If a request doesn’t HIT the cache, a PHP worker will take and process the request, and then return it to the visitor in the form of a webpage.

Their ability to function isn’t infinite – it depends on various factors including the requests (codebase, database queries), and the server resources available to them which will determine how many uncached visits/requests your site can handle at a time.

Browser < > Nginx < > PHP < > MySQL

### PHP and Web Hosting

In a web server environment, PHP is single-threaded, which means that a PHP process can only run on one CPU core, and it can’t span multiple cores. You can have multiple PHP processes running, one on each core, but a single process itself can never use more than one core.

For example, if you have 3 requests and one CPU core, PHP workers form a queue and the requests are processed one at a time. Once a PHP worker goes to work it focuses solely on that task for the entire duration of that request. If one of those 3 requests takes a long time to complete, it can result in slow load times or 504 errors at that moment in time.

If you’ve ever received a seemingly random 504 error that was quickly gone after hitting refresh, this may well have been the cause.

If you have 3 requests and 4 CPU cores, then these can all run at the same time, 1 per core, and you’d still have one CPU core available.

Side note: While technically PHP can be extended to offer multi-threading via the pThreads extension, the pThread extension cannot be used in a web server environment. Threading in PHP is therefore restricted to CLI-based applications only. Source: PHP Manual.

### PHP Workers and WordPress

WordPress itself is a single-threaded application. This means that one WordPress request (page load, search request, product filtering, etc), no matter how complex, is handled by one PHP worker. Multiple PHP workers do not get involved in different facets of one WordPress request.

One request, one PHP worker, one CPU core.

Here’s an example of your average simple request:

 

## Part 2. Server Resources and PHP Worker Limitations

Before you can begin fine-tuning your PHP workers for optimal performance, you first need to understand how your available server resources affect the number of PHP workers that you’ll be able to use.

More PHP workers doesn’t mean better performance. In fact, too many could literally consume all of your resources and tank your server. In contrast, too few workers could cause 502 errors on your sites even though your server has plenty of available CPU and RAM and could handle greater workloads.

The number of CPU cores and the quality of your website’s code (poorly written code requires more work to process) are both more important factors than the number of PHP workers. Your goal is to strike the right balance so that your server has the “optimal” number of workers to perform at its very best.

### The Problem with too many PHP workers

As each PHP worker is its own computing process, so even when idle it requires some resources to exist as a process. The more PHP workers in existence, the more resources are required to sustain them – this can have a significant effect on RAM, so it’s particularly important on smaller servers where the OS, and microservices utilize a higher percentage of available RAM.

A 1GB RAM VPS for example, isn’t going to have a lot of usable memory left over after everything else that’s fundamental to your servers operation has taken up its share.

Also, if you have too many PHP workers for the available CPU, when your server starts hitting 100% CPU capacity, having those extra PHP workers is going to cause additional problems. Your system will become increasingly ineffective, resulting in an excessive number of processes, which can, in turn, cause each process to take longer and longer to complete. It’s highly likely that at that point that your visitors will begin experiencing 503 errors, and worse case scenario your system is going to fail.

The bottleneck here is too few CPU cores.

### The Problem with too few PHP workers

As mentioned earlier, too few PHP workers means your server has the resources to take on more work, but you don’t have the workers to get the jobs done – not enough PHP workers is the bottleneck. It’s essentially self-sabotage. If your site is performing poorly but your CPU isn’t coming close to 100% capacity, you should look at increasing the amount of PHP workers.

### Finding the sweet spot

This could be considered more art than science.

I wish we could just give you a magic number like 4 workers per CPU core (which is actually a good starting point and what we recommend), but it’s not always that simple. The ideal range for your websites may vary significantly, and could be anywhere between 2 workers per core to 8 workers per core depending on the amount of PHP processing required and the quality of the CPU. This largely depends on your websites code base and the type of tasks that are being performed. Generally speaking, the more complex the tasks, and/or the lower quality the code base, the fewer PHP workers should be set per core.

Finding the right number for you may take some experimentation, but what you’re looking to achieve is for the CPU capacity to hover between 80-100% under load.

### PHP Workers and CPU Performance

Due to the fact that one request is handled by one PHP worker on one CPU core, opting for the best possible single-thread performance is a good idea when it comes to hosting more dynamic websites (meaning you should go for servers with the higher performance CPUs for WooCommerce, Learning Management Systems etc). The more dynamic a website is, the more PHP is required to get involved in handling requests, and the better your CPU performs, the faster your PHP processes can be… processed.

If you’re a designer, you may have experienced something similar when trying to use something like Photoshop on your old laptop vs Photoshop on your shiny brand new upgrade. Things just get done way faster because your newer CPU can process faster. OR perhaps you even noticed the difference in speed in simply booting your laptop up (or desktop or whatever).

CPU performance should be a consideration when putting your hosting proposals together. For your average WordPress site, it’s not going to make a world of difference. Even Lightsail can be fine for low traffic sites. For your more complex dynamic sites however, you may be much better off with Vultr High Frequency, Google Cloud Platforms compute-optimized C2, or a gaming server from OVH.

This is one of the reasons that Vultr High Frequency has become so popular so quickly. Their CPU performance is, dollar for dollar, pound for pound, the best on the market right now in 2020. Data from testing UpCloud shows their performance is also excellent and well worth your consideration. They also have a great track record for uptime, which may be a more important factor in some cases.

For dynamic websites like ecommerce, where you have uncached traffic once a customer begins adding items to their shopping cart, you’ll see better performance having a stronger CPU, especially under load.

### Managed WordPress Hosting Limitations

Part of the problem with most managed WordPress hosts is their billing metrics. The PHP worker limitation in particular is a serious problem when working with these hosts because this way of operating is built directly into their infrastructure. Your plan includes a set PHP worker limitation per site. If you need to tweak your PHP workers for better performance, well… you can’t. You’ve hit your limit, and even if their support team is top notch, their hands are tied and they literally have no choice but to sell you a higher plan. There is no other solution, and so you’re punished for having a well optimised site.

That’s shit. Seriously.

It’s also why many people using these hosts end up on much, much more expensive plans than they would otherwise require. Many of our own clients become our clients for this very reason, and this is an experience that many, many agencies have in common.

PHP worker limitations and bullshit metrics like pageviews are just two of the many reasons WordPress agencies are making the move to GridPane, where instead of being arbitrarily taxed on their success, they can instead benefit massively from the unrestricted economies of scale that comes with managing their own servers directly.

 

## Part 3. WordPress Performance and PHP Workers

In this section, we’ll take a look at factors that affect performance at the individual website level. The quality of your website’s code, the amount of dynamic content you serve, and the complexity of the tasks PHP needs to process, all affect the CPU-PHP worker balance.

Every website has different themes, plugins, and functions, and these all affect performance and the amount of work PHP workers need to do when serving content to your website’s visitors.

### The Importance of Caching

Caching is key to a high-performance WordPress website. If a page isn’t serving dynamic, visitor-specific content, then it should be cached, and this is best handled at the server level. Web servers like Nginx and OpenLiteSpeed offer exceptional performance when serving from the cache, and both are capable of handling a MASSIVE amount of concurrent traffic when PHP processing is kept to a minimum.

When a page is cached, what it’s storing is pre-prepared HTML, CSS and JS that’s ready for a browser to use immediately. Nginx / OpenLiteSpeed don’t need to send anything to PHP for processing in order to “create” a page as they simply stored a copy of the result from the first time it was created. At this point, it’s just like serving a completely static website.

Taking away the need for PHP (or MySQL) to do any work, means the server has to do significantly less to deliver the same result.

Here you go dear visitor, here’s what we made earlier!

Which brings us to…

### Dynamic WordPress Websites

In part one we talked about requests that “BYPASS” or “MISS” your website’s cache and how PHP workers need to be involved to serve these requests.

Dynamic WordPress websites are those where the cache is regularly BYPASSed, meaning Nginx / OpenLiteSpeed aren’t serving a pre-prepared set of HTML/CSS/JS. For example, if you add an item to a shopping cart, this is dynamic data that we purposely do not want to cache, and for this item to stay in the shopping cart for only this one individual visitor, this requires personalised, cache BYPASSing content.

The most common types of dynamic websites are: –

GridPane is particularly popular with large WooCommerce and LMS websites due to the PHP worker configuration options available, and the ability to choose IaaS providers with high-performance CPUs at their base cost – we don’t add any markup or making any money whatsoever from your servers.

These options allow for maximum flexibility and performance, without any of the restrictions or immense costs associated with the high-tier plans at most managed hosting providers.

Dynamic websites are going to require more PHP workers and server resources for those PHP workers than regular brochure style websites for the same amount of traffic. Serving logged-in visitors or visitor specific content requires PHP for every single request, and so you need to assess and plan for these types of websites differently than you would an average website.

### The Quality of Your Code Base

The quality of your website’s codebase is going to play a significant factor in how much work a PHP worker has to do in order to finish each individual request.

Better/High quality code = faster processing.

This becomes even more important when the requests themselves are complex. For example, filtering a large WooCommerce catalogue requires some significant processing from both PHP and the database, and if your codebase is poor to begin with, this will require more and more server resources as you scale to accommodate it.

On the flip side, if you have a lean, super clean code base, the amount of work required to process the same type of request is significantly less, which means more tasks could be accomplished in faster time, by few workers.

If possible, it’s always best to start with a lightweight, modular theme, and then do your best to vet the plugins you’re using and opt for the most lightweight option for what you’re looking to accomplish. On top of that, you can also use plugins such as Asset CleanUp, Autoptimize, Fast Velocity Minify, Flying Scripts, or Perfmatters (premium only) to reduce requests further.

If you have an existing site that’s profitable but underperforming, getting expert assistance to help you speed up your site can be a great investment.

### Task Complexity

Complex database searches such as filtering a clothing catalog based on different categories (for example, male winter coats that are blue and under $60) is a significantly more complex, and thus resource expensive task, than simply loading a page that hasn’t been cached.

If your website experiences a lot of complex tasks these will limit your performance. Ensuring that your codebase is as lightweight as possible will help lessen the burden.

### PHP Version – You should be using PHP 7.4 or higher

If you want to increase your website’s performance, then you should be using at least PHP 7.4 for all of your websites. 7.4 is the fastest available version at the time of writing, but 7.3 has more overall compatibility with some plugins. Use whichever works best for you.

If you’re not using at least PHP 7.4, it’s time to upgrade – like ASAP (all previous versions have reached their end of life and will never receive another update/security patch). If your web host doesn’t support 7.4 or higher, that’s a pretty strong indicator that you should find a new host as they simply don’t take their business or your business seriously.

##### What About PHP 8?

At the time of writing, PHP 8 is still a wildcard. Adoption among most popular plugins has pretty much rolled out across the board, but there are still many that haven’t and these may result all kinds of odd behavior or even break your site if that’s the case.

If you’re interested in learning about PHP 8 and WordPress, I highly recommend you join the big WordPress Hosting Facebook Group and watch this video.

We will update this post in the future.

 

## Part 4. Nginx, OpenLiteSpeed and Different Worker Types

Different webservers have different worker types, and this means the options for tuning them differ. Below we’ll take a look at the different worker types on both Nginx and OpenLiteSpeed, and the terminology you need to understand before you can begin making changes to them.

We’re not going to look at Apache because this guide is for WordPress and it’s 2021.

### PHP Workers and Nginx: FastCGI Process Manager (FPM) Types

On most Nginx web servers, PHP workers are handled by the FastCGI Process Manager – which you’ll often see abbreviated as PHP-FPM. Using PHP-FPM you have three options to: ondemand, static, & dynamic.

We’ll dig deeper into each of these options and their use cases in part 5.

### Nginx Worker Settings

Below details the different settings available for configuring your PHP workers. “Children” refers to PHP workers. These are the settings you’ll be adjusting when it comes to tuning your workers for optimal performance. Some of these settings are specific to Dynamic and Ondemand modes.

pm.max_children: The maximum number of children (workers) that can be alive at the same time.

pm.start_servers: The number of children created on startup.Dynamic mode only.

pm.min_spare_servers: The minimum number of children in ‘idle’ state (waiting to process). If the number of ‘idle’ processes is less than this number then some children will be created.Dynamic mode only.

pm.max_spare_servers: The maximum number of children in ‘idle’ state (waiting to process). If the number of ‘idle’ processes is greater than this number then some children will be killed.Dynamic mode only.

pm.process_idle_timeout: The number of seconds after which an idle process will be killed.Ondemand mode only.

pm.max_requests: The number of requests each child process should execute before respawning.

Source: https://www.php.net/manual/en/install.fpm.configuration.php

### PHP Workers and OpenLiteSpeed: PHP LSAPI

LiteSpeed and OpenLiteSpeed run PHP LiteSpeed SAPI, which is a custom version of PHP specific to LiteSpeed Web Servers.

Just like Nginx, OpenLiteSpeed offers a number of different PHP process modes via PHP LSAPI: ProcessGroup mode, Daemon mode, and Worker mode.

Source: https://www.litespeedtech.com/support/wiki/doku.php/litespeed_wiki:php:process-mode

The above documentation from LiteSpeed is well worth reading for a deeper understanding of how PHP Process Modes work, as well as their pros and cons.

### GridPane and Daemon Mode

Daemon mode does not allow the use of custom per-user php.ini, and so individual websites can’t be customized. This is a common choice for shared hosting environments, but due to its customization limitations, this option isn’t available on GridPane.

### OpenLiteSpeed and “External Applications”

OLS/LiteSpeed documentation isn’t particularly intuitive for anyone who doesn’t already have a lot of LiteSpeed experience. Throughout their documentation, you will see it refer to “external applications”. LiteSpeed web server (LSWS) supports seven types of external applications. These are: –

This guide is specific to WordPress. In LiteSpeed and OLS, WordPress uses the external app type “LiteSpeed SAPI application” to have PHP communicate with the web server.

With the exception of “Web server”, which GridPane makes use of to proxy Monit, none of the other applications are needed when it comes to hosting WordPress websites.

When you see OLS documentation refer to “external application” in the context of PHP workers, they are referring to LiteSpeed SAPI application, and to be more specific, PHP LSAPI (also referred to as LSPHP).

Learn more here: https://www.litespeedtech.com/open-source/litespeed-sapi/

### OpenLiteSpeed Worker Types

Before we look at the individual settings, this explainer directly from the LiteSpeed docs breaks down the difference between the Worker and ProcessGroup worker types as they relate to LSAPI Children and LSAPI App Instances settings:

“Setting LSAPI_CHILDREN to 1 puts LSWS in Worker mode. In Worker mode, LiteSpeed Web Server dynamically spawns new PHP processes to meet demand and kills finished processes.

Translation: In Worker mode, the server will create PHP processes as needed, and then kill them when they are no longer needed. Similar to PHP-FPM Ondemand.

Setting LSAPI_CHILDREN to a number larger than 1 puts LSWS in ProcessGroup mode. In ProcessGroup mode, the web server will start one constantly-running PHP parent process. This process will then fork child PHP processes (as opposed to spawning new processes) to meet demand. ProcessGroup mode is generally preferred because all PHP processes can then share one memory block for opcode caching. In ProcessGroup mode, Instances should be set to 1, while LSAPI_CHILDREN should be set to match the value of Max Connections.”

Translation: In ProcessGroup mode there is always one PHP parent process running, and to take on more PHP tasks, it will fork child processes, which is much more efficient than generating new processes.

If you’re a GridPane client, you’ll see that when you change the LSAPI Children in ProcessGroup mode, the Max Connections will automatically match. In Worker mode, the LSAPI app instances will automatically match the Max Connections.

PHP LSAPI Children: The maximum number of child processes that can exist at any one time (one parent PHP process is always in existence).

PHP LSAPI App Instances: The number of PHP processes that can exist at any one time.

PHP LSAPI App Max Connections: This specifies the maximum number of concurrent connections that can be established between the server and PHP LSAPI, and how many requests can be processed concurrently.

PHP LSAPI Initial Request Timeout: This specifies the maximum time in seconds the server will wait for PHP to respond to the first request over a new established connection. If the server does not receive any data within this timeout limit, it will mark this connection as bad and return a 503 error.

This can help identify communication problems between OLS web server and PHP as quickly as possible. If you have legitimate, long-running requests, you can increase this limit to avoid 503 error messages.

PHP LSAPI Retry Timeout: The period of time (in seconds) that the server waits before retrying after a prior communication problem.

PHP LSAPI Max Reqs: The maximum number of requests each child process will handle before automatically exiting. When one process exits, another will be created. This is necessary in case any PHP functions have memory leaks, which could become highly inefficient.

PHP LSAPI Max Idle (Seconds): The maximum idle time before a PHP process is stopped by the server. This setting allows resources used by idle applications to be freed up after a set amount of time has passed.

https://www.litespeedtech.com/support/wiki/doku.php/litespeed_wiki:php:lsapi-environment-variables

 

## Part 5. Example Use Cases and Building Your Own Hosting Services

Alrighty, with the foundations all covered, let’s look at how to begin putting all of the above into practice. Below we’ll look at the different goals you need to consider ahead of time, and then some examples of how to begin tuning for different types of sites. Below we’ll look at:

### Basic Guidelines for Nginx

At GridPane, our default setting is to use Dynamic PHP workers on Nginx, and our defaults for each worker type are as follows: –

Our default Dynamic settings are going to work very well for 90% of all the sites that are hosted on our platform. This means your average, well-cached website that has minimal dynamic content.

 

 

### Tuning OpenLiteSpeed Performance

We will add tuning recommendations for high traffic dynamic websites in the future. For all other scenarios we recommend the default ProcessGroup worker settings.

### ProcessGroup vs Worker Mode

Unless you have a very specific reason for using the Worker process mode, we recommend you stick with ProcessGroup for all your websites. Our default settings are based on LiteSpeed's recommendations and these will serve you well, no matter what type of website you’re hosting.

### Hosting a simple WordPress Website

I currently host my personal site on a nice little 2 CPU core, 2GB e2-small instance at Google Cloud Platform, totally free of charge courtesy of their $300 12 months free credit. It’s pretty great, and since it shares no resources with any other sites, is completely static, takes advantage of server-level page caching and Redis object caching, it could handle a massive amount of traffic if it ever needed to. It’s overkill to be honest, but free is free.

The default dynamic setting of a minimum 1 worker per CPU core at all times is totally adequate, and the server will create up to a maximum of 4 per core should it ever need to. In my case, I could use ondemand, static or dynamic and it would make little difference.

When hosting a simple website, or a handful of simple, well cached, low traffic websites on a server, PHP workers generally aren’t something you’re going to need to worry about, but dynamic is a very safe bet.

### Hosting A LOT of simple, low traffic websites on one server

If you’re hosting A LOT of low traffic websites that are all making use of server level caching, then using ondemand workers for these websites may serve you best, but dynamic still may be best.

For example, if you were hosting 50 websites on a 4 CPU core server, all with dynamic workers active set to one worker, that’s 1 worker per website. Here we’d have a total of 50 active PHP workers on this server at all times, permanently taking up resources. This of course would be orders of magnitude worse if all these websites were using static workers. On static, at 3 workers per core, that’s 600 active PHP workers! That’s a bad idea.

You will need to keep an eye on the total number of max children of all sites combined, and the PHP max memory per script.

As they’re all low traffic sites, they will function perfectly well using ondemand, allowing the server to create workers as needed, and then killing them once their watch has ended. And, by conserving resources, you’ll be able to host more websites per server if that’s your goal (but we’d still recommend not stuffing a server with as many websites as possible, and instead spread them out and use dynamic).

##### A Better Alternative

7-10 brochure style websites per 1 GB of RAM is a good guideline for how many of these sites a server can handle. Following this guideline, go ahead and use dynamic (our defaults are perfect if your a GridPane client).

### Hosting one super-high traffic website

If you’re hosting a super high traffic website, then there’s a few things that you’re probably going to want to do:

It’s more important to plan for maximum concurrent traffic. 100,000 visitors spread out throughout the day is a very, very different hosting problem to 100,000 visitors per day but that all hit your website at the exact same time.

Here our website isn’t sharing any resources, so the server can easily afford the use of static workers. There’s no downside, so start off with 4 workers per core.

### Hosting a high traffic WooCommerce website

eCommerce presents its own unique challenge. Requests frequently BYPASS the cache, and there are extensive PHP and database queries. For these types of heavy workloads, it’s best to host these websites on their own server.

You’ll also want to make use of object caching to reduce the workload on your database. This will be a significant performance booster for any MySQL heavy website. Your server’s available RAM should also be at least double the size of your database.

The larger the store in terms of product inventory, typically there’s going to be more work on PHP and the database as your visitors search for and filter products to find what they’re looking for. WooCommerce also is far from the leanest codebase to begin with…

A good place to start for many eCommerce sites is using static workers at 3 workers per CPU core. If you have a clean code base and aren’t dealing with too many long-running requests, test how it performs at 4 and 5 workers per core until you find the sweet spot.

### Hosting a high traffic LMS / Forum / Membership website

These types of websites all share the same primary problem: Logged in users.

As soon as a user logs in to WordPress, they’re now BYPASSing the cache, and so everything they do on your site needs to be processed by PHP and MySQL.

If you have a lot of people active on your site at any one time, this could put a lot of strain on your system as PHP workers are responsible for everything.

In these cases, you’ll want your codebase to be as lean as possible, and host the site on its own server with a high-performance CPU. You’ll also want to use Static workers.

Begin testing static workers at 3 workers per CPU core, monitor how things are going during periods of high loads, and test how your site performs at 4, 5, and maybe even 6 workers per core until you find the sweet spot.

### Hosting a WaaS / Multisite Network

Your WaaS network should be fully cached and on its own server. The same principle applies here – one website has access to all the resources, so going with Static workers will provide the best performance on both the front and back end.

Additional note: Adding eCommerce into a multisite network is a very bad idea. Not only from a performance standpoint (which could be highly problematic as people begin shopping across different stores) but also from a security perspective. If one store were to ever get compromised, all stores in your network would get compromised and it is not worth the risk to your business, or your customer’s business, or to their customer’s private information.

There is no upside.

We highly recommend that you avoid any type of eCommerce on your WaaS networks. If needed, move the few clients that do require it to their own stand-alone WordPress installations (and charge them more).

 

## That’s a Wrap

PHP workers are an advanced and dense topic, but one that is well worth your time. We hope you’ve found this to be a valuable read and we would love to hear your feedback and suggestions on how we could make it even better.

Let us know your thoughts in the comments below!

 

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

### 9 Comments

## Leave a ReplyCancel Reply

Your email address will not be published. Required fields are marked *

Name  *

Email  *

Website

Please check the box below to consent to the processing of the submitted personal data in accordance with our Privacy Policy, including the transfer of data to the United States.

I have read and accepted the Privacy Policy
		 *

Add Comment *

Post Comment

 

 