# What Size Servers to Choose and When to Scale Servers Up | GridPane

# What Size Servers to Choose and When to Scale Servers Up

 

11 min read 

 

### Information

You may also be interested in this getting started article: 
Getting Started: Choosing Your First Servers and Common Server Questions

### Table of Contents

 

## Introduction

When first getting started managing your own servers, you may have questions about what size servers you should choose, and how many websites you should host per server. This article will explore the topic in-depth and give you the information you need to make these decisions for your business.

There are no definitive answers to these questions. Everything depends on your website’s codebase, caching, the number of concurrent visitors, how those visitors interact with your websites, and the specs of a given server.

That said, once you know the variables, it’s just a matter of knowing when it’s time to scale up. We’ll take a look at this too.

 

Part 1: Factors that Influence Server Choices and Sizing

 

## CPU, RAM, and Storage

When choosing your servers, these are the 3 variables that will drive your decision-making.

RAM and disk space are straightforward. How many sites? How big are their databases? How big are their uploads folders? You’ll want enough to cover this, plus extra to cover system resources, and then extra to spare.

CPU is more complicated as it depends on the workload the server needs to be able to handle, and numerous factors influence this. Without real-world data, the [unhelpful] answer to many CPUs you need is: “it depends.”

 

## RAM Guidelines

RAM will likely be the main consideration when creating most of your servers.

The amount of RAM you need is primarily determined by the size of your website database/s. Hosting a 5GB database on a 2GB RAM server is not a great idea for performance.

### Variables

Variables that affect the amount of RAM you need are primarily:

If your website is growing, you’ll want to ensure your server has plenty of room to accommodate that growth.

### Guidelines

 

## CPU Guidelines

The two main variables that affect CPU are:

Snapshot Failover and UpdateSafely will both impact this as well if enabled.

### Website Load

This depends on your traffic and your codebase.

How lean your codebase is, the type of requests being processed, and fast your CPU cores can handle these requests will affect how much CPU power a given workload will require. RAM frequency and disk speed also play a role – the faster these are, the better so that the CPU isn’t waiting on them.

This is why it’s easy to cater for fully cached, low-traffic sites but more complicated to estimate the server power needed for WooCommerce, LMS, Buddyboss, etc.

### Backups and Other Features

Backups, cloning sites from one server to another, and running UpdateSafely are all CPU-intensive tasks. If you have 40 sites on a server and they’re all backing up every hour, then you may want more than 2 vCPU cores to handle this workload.

For Snapshot Failover and UpdateSafely, it depends on the frequency.

If you regularly have a lot of GridPane tasks running simultaneously every day and you consistently see CPU spikes, then you may want to scale this server up.

 

## One Big Server vs. Multiple Smaller Servers

Generally, it’s better to spread your risk across several servers at different data centers so that should one ever go down, not all of your sites go down.

Dealing with trouble tickets for site outages from unhappy clients is time-consuming and exhausting. All of your websites going down at the very same time is an unnecessary risk that’s easily preventable.

Spreading your sites across 2 CPU 4GB RAM servers is generally the sweet spot.

The 7-10 sites per GB of RAM rule is mainly for the 90% or more WordPress websites that are functionally static brochure sites that get fewer than 1000 visitors daily.

Don’t put all your eggs in one basket. This is our official recommendation.

 

## Minimum Server Specification Recommendations

We recommend servers with at least 2GB of RAM as a bare minimum. Typically on these plans, you’ll get 1 CPU and around 50GB of SSD disk space for $10-12/month.

2 CPUs and 4GB RAM would be better.

 

Part 2: General Advice for Different Use Cases

 

## Static “Brochure” Websites

Below are very general guidelines. Everyone’s websites are different, with different traffic, plugins, themes, admin usage, etc.

As a general rule, 7-10 websites per 1GB RAM will work well in most cases. Most GridPane users (myself included) tend to be a little more conservative and go for somewhere in the range of 20-30 websites per 2 CPU 4GB RAM server. The value at this price range is excellent, and that extra CPU can make a huge difference.

Server space is also cheap, and that’s definitely a good number to shoot for if all of your websites are fully cached and primarily static. It does of course vary, and these are only guidelines.

For static, brochure sites that are all fully cached, there’s really no need to go above a $40-$48/month plan (approx 4 vCPUs 8GB RAM), and you may be better off splitting your websites over multiple baskets.

 

## WooCommerce

Many Woo stores are small and get very little traffic. For example, I host a site for a photographer that offers around 300 prints for sale. It’s a low-traffic site and doesn’t make a huge amount of sales. The site doesn’t take up a considerable amount of disk space, and the database is still relatively small. I treat this site no different than my other brochure sites, and it shares a server with a bunch of them.

### Large Databases

If you’re hosting a site with a large database, then ideally, you want the amount of RAM to double the size on 8GB RAM servers or less. More than this, and you don’t really need double, but you will want adequate available RAM for the Redis Object Cache and system resources, including PHP workers.

Large stores should ideally be hosted on their own servers with their own resources.

### High Traffic WooCommerce

Woo sites that get a lot of cache bypassing traffic require more CPU power than your average fully cached brochure site. Each time a page load bypasses the cache, that page needs to be built from scratch instead of returning the “here’s what we made earlier” version from the cache. WooCommerce is also particularly heavy on MySQL.

It’s difficult to give advice for these types of sites without knowing more about the site, how much cache-bypassing traffic it gets, and how heavy the codebase is. Start with 2 CPUs and 4GB RAM, monitor your CPU and RAM usage and notifications, and scale up from there as needed.

Many who move their busy sites from managed WordPress hosts to GridPane find that their sites that require very, very expensive hosting plans perform remarkedly well on a 4 CPU 8GB RAM server.

### Further Thoughts

Ideally, these websites are better off with their own resources. However, if they are low-traffic, you could share 2-4 CPU servers with a handful of other low-traffic Woo sites. E.g. 3 small, low-traffic Woo stores on a 2 CPU 4GB RAM server.

We also have a dedicated article on working with WooCommerce here: Working with WooCommerce on GridPane

 

## Learning Management Systems (LMS), BuddyBoss, and Membership Sites

These websites are similar to WooCommerce in many ways, and the same considerations apply – please be sure to also read the section above.

You need to plan for concurrent cache-bypassing users. When users are logged in and making their way through a course or making any kind of updates, these requests can all be very MySQL intensive, and high concurrency can consume a tremendous amount of CPU.

Buddyboss, in particular, is a heavy codebase to run, plus all the extensions and an LMS that usually go with it.

Any LMS or Buddyboss site that’s making money should live on its own server and have its own resources. Start with a 2 CPU 4GB RAM and scale up from there.

 

## WaaS Networks

Start out on a 2 CPU 4GB RAM server and scale up as needed. Even large networks don’t experience a great deal of cache bypassing traffic in the form of subsite owners spending lots of time logged in.

Your database size and upload folder size can both grow rapidly, though, so be sure to keep an eye on your Monit notifications for RAM and Disk Space warnings.

We have a dedicated article on growing your WaaS business that you can view here:Scaling Your WaaS Network: Advice for WP Ultimo, and Multisite vs Multitenancy

 

Part 3:  When to Scale Up

 

## Scaling Factors

The same factors that influence what servers you choose to start with will help you determine when you need to scale up. Each of your GridPane servers comes with Monit, and this provides you with the information you need.

### CPU

If you’re seeing CPU spikes at specific times, this may be due to lots of backups taking place set to take place at the same time. You may be able to reduce these warnings by spreading out your backup times.

### RAM

If PHP is taking up a large amount of RAM, then this may be due to having an excessive amount of PHP workers. You may want to limit these as outlined in the guidelines of our PHP worker article and also reduce any workers on your staging sites to free up space:PHP Workers and WordPress: A Guide for Better Performance

### Disk Space

You should always have ample disk space available, which is more of a concern on smaller 1-4 CPU servers. If you’re getting high disk space warnings, you should either scale up straight away or investigate and remove unnecessary files and old backups to free up space.

Running out of disk space can cause irreversible database corruption, and you’ll need to use a server provider snapshot to recover. Here’s a guide on troubleshooting high disk space: Troubleshooting High Disk Space Usage and Locating Large Files

 

## Load Testing Considerations

Load-testing a regular static site that’s fully cached probably isn’t worth your time or effort. If you’re not getting millions of visitors per month, then you probably don’t need to worry too much about it.

When load testing anything else, you need to be able to replicate the kind of load that you’re expecting.

Running a load test that simply loads pages when the actual load to be concerned about is your LMS students saving their course progress to the database is not going to give you reliable data that can be used to estimate what size server you really need accurately.

The same goes for high-volume concurrent WooCommerce checkouts or Buddyboss interactions.

Understanding the expected workload and emulating it must be the goal of your load testing.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

