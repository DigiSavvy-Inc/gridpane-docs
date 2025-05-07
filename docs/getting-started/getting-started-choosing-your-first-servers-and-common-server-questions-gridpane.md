# Getting Started: Choosing Your First Servers and Common Server Questions | GridPane

# Getting Started: Choosing Your First Servers and Common Server Questions

 

11 min read 

## Introduction

When first getting started managing your own servers an entire world of new, incredibly cost-effective options are now open to you. This can be a little overwhelming in the beginning, and some of the common questions that you may yourself have as well include:

In this article, we’ll offer some guidance on how to choose the right servers for your business, as well as some general strategies that will help answer the most common questions that we see.

### Table of Contents

 

## Choosing Your First Provider

The short version is if in doubt, we typically recommend Vultr. Specifically, these two server types:

Both offer excellent performance.

### Vultr

Vultr has a fantastic offering with their High-Frequency lineup. Dollar for dollar, they have the best performance right now in the $6-$24 price range. They also have an excellent set of data centers and have even more planned.

They’ve been the most innovative in the space that they compete in for a few years now.

### DigitalOcean

Excellent uptime, performance, and you can easily scale your CPU and RAM up and back down again if you ever need to do so (e.g. for short busy periods where you’re having a sale, or launching a product etc). Everything is just easy with DigitalOcean, and they have a datacentre in Bangalore, India, which may be particularly useful if you operate in India or nearby countries. Their premium droplets are great value for money and offer excellent performance. The AMD option has performed a little better from the tests we’ve seen, but the Intel is still great too.

### UpCloud

UpCloud has excellent uptime and particularly good (and fast) support. You can scale resources up and then back down again as long as you don’t increase disk space, and that can be particularly useful when expecting short periods of high traffic. Their European datacentre location options are pretty stellar.

### Linode

Linode offers a stable and reliable service. The CPU you get may vary though. You may get a decent AMD CPU, or you may get an older, less performant CPU. That’s unfortunate, but even still they’re a solid option. What I personally really like from them is their dedicated CPU plans. You can also scale up CPU and RAM, and later scale back down again.

### Amazon Lightsail

As you probably noticed, Lightsail did not make our shortlist above.

While we have an integration with Amazon Lightsail, as data has rolled in, the four other providers above offer much better value for money when it comes to performance. What Lighsail does offer is great uptime, a good choice of datacenter options, and above-average disk space, but their specs aren’t particularly great, and they throttle CPU usage in a way that is kind of crazy – they don’t like you using above 20% per CPU.

The bottom line is that it’s plenty good enough if you have Amazon credit and your hosting simple, fully cached sites. If you’re spending money though, dollar for dollar you will get better performance at DigitalOcean,  UpCloud, Vultr, and Linode.

 

## Minimum Server Specification Recommendations

As a bare minimum, we recommend servers with at least 2GB of RAM. Typically on these plans, you’ll get 1 CPU, and around 50GB of SSD disk space for $10-12/month.

2 CPUs and 4GB RAM would be better.

While we have hundreds of servers connected to GridPane with 1 CPU that run absolutely fine, one thing that can happen is that tasks that can take a while to complete, such as backups, cloning, or just inefficiencies in one websites codebase, can hold up other important tasks from having access to the CPU, potentially causing occasional 502/504 errors at seemingly random times.

Such issues, even though rare and never happen in most cases, are significantly less likely to occur when there’s an additional CPU available and not all tasks need to wait on access to 1 sole CPU.

 

## Uptime Track Record

Super important, perhaps more than any other factor. The last thing you need is to be swamped with complaints because a datacenter goes down for an extended period of time.

Any server you purchase should be from a provider with a solid uptime track record. A good third party for checking these things is Cloudharmony who monitor a variety of IaaS providers and their services:

Cloudharmony Status

 

## Datacenter Location

The location of your datacenter matters. It’s one of the easiest and most overlooked ways to speed up your load times.

Wherever possible you should always host in a datacenter that is as close to your website visitors as possible.

If you have a more global audience, you could consider a CDN, but Cloudflare’s free plan and hosting as close to where the majority of your traffic comes from is usually enough.

One of the benefits of using GridPane is that you can connect almost any quality VPS, VDS, or dedicated server to our platform, so there’s always a server close by.

One of our awesome community members created this map that shows the locations of our current providers that you may want to bookmark: https://www.glimmernet.com/gridpane-server-locations/

 

## Which Ubuntu Version?

GridPane will support each new major Ubuntu release once the necessary packages are available for them. Our server provisioning documentation will state which versions are currently supported.

We recommend you always choose the most up-to-date version for new servers due to the additional years before it will have before reaches its end of life (EOL).

 

## Nginx or OpenLiteSpeed?

This is a massive topic all by itself, and there’s no right or wrong answer.

OLS caching is easier to configure, and it comes with a .htaccess file. These are typically why people prefer OLS over Nginx.

If you were hosting something considered “Enterprise” then we typically recommend Nginx – it’s battle-tested, performs exceptionally well, and is more stable as a platform. Also, despite all the performance claims of LiteSpeed/OpenLiteSpeed vs Nginx, the highest traffic WordPress sites in the world run on Nginx – including the highest sites I’m personally aware of on our platform.

Whichever you choose, you’ll get excellent performance out of both. Why not spin up a server using each and test them out for yourself?

 

## Percona or MariaDB?

The two options exist because some people have a preference for one over the other. In terms of performance, this one probably isn’t going to move the needle for you.

Personally, I tend to stick with Percona, but for a large scale dynamic website (WooCommerce, LMS, BuddyBoss, etc) you may potentially eke out a little better performance with MariaDB. Maybe.

If you don’t already have a preference, you may want to choose one or the other and stick with it across all your servers. Moving sites between Percona and MariaDB should cause no issues.

 

## Server Snapshots/Backups

We highly recommend that you take advantage of your server provider’s snapshots (aka server backups). You will likely never have to make use of them, but if you ever did, it is probably the best insurance you will have ever invested in for your business.

These are usually an additional 20% on top of the base price.

You can learn more about our recommended backup strategy here:GridPane’s Recommended Backup Strategy

 

## How Many Sites Per Server?

Below are very general guidelines. Everyone’s websites are different, with different traffic, plugins, themes, admin usage, etc.

### Static, Fully Cached Brochure Websites

As a general rule, 7-10 websites per 1GB RAM can work well. Most GridPane users (myself included) tend to be a little more conservative and go for somewhere in the range 20-30 websites per 2 CPU 4GB RAM server. The value at this price range is excellent and that extra CPU can make a huge difference.

Server space is also cheap, and that’s definitely a good number to shoot for if all of your websites are fully cached and mostly static. It does of course vary, and these are only guidelines.

Generally, it’s better to spread your risk across several servers so that should one ever go down, not all of your sites go down.

For static, brochure sites that are all fully cached, there’s really no need to above a $40-$48/month plan (approx 4 vCPUs 8GB RAM), and you may be better off splitting your websites over multiple baskets.

### Woo, LMS, Membership, Forums, etc

For sites that are dynamic in nature and get a lot of cache bypassing traffic, these can require a lot more CPU power than your average fully cached brochure site. Each time a page load bypasses the cache that page needs building from scratch instead of returning the “here’s what we made earlier” version from the cache. WooCommerce and LMS are also particularly heavy on MySQL.

It’s difficult to give advice for these types of sites without knowing more about the site, how much cache-bypassing traffic it gets, and how heavy the codebase is.

If they’re very low traffic then they may be fine alongside your other brochure sites. Ideally though, these websites are better off with their own resources, or, if low traffic, they could share 2-4 CPU servers with a handful of other low traffic sites of the same kind. E.g. 3 small, low-traffic Woo stores on a 2 CPU server.

For more specific advice, reach out to the community and let us know more about your websites:

https://community.gridpane.com/

 

## What About Other Providers?

For most of your servers, the providers we natively connect with will serve you extremely well. You may never need to look elsewhere.

That said, there are of course many, many options out there and the server world really is your oyster.

Two other popular providers that don’t have an API integration with are Hetzner who have server locations in Germany and Finland, and OVH who are as global as they come.

### Hetzner

Hetzer are definitely worth a look, especially if you’re in Europe. Their pricing is awesome, they have great support, and they have been around for a long time. They have all kinds of servers at all different price points, from small VPS offerings to dedicated AMD Ryzen gaming servers.

We have this knowledge base article on how to use them with GridPane:

Provision a Hetzner Server using our Custom Server Option

### OVH

OVH has one of the largest selections of servers in the world, and offers everything from low-cost VPS to high-end gaming servers, to massive enterprise servers.

Their Infra 2 Gaming Servers in particular offer exceptional performance and are great value for money. When you have a WooCommerce store, LMS, Membership site, or WaaS that’s grown to the point where you’re looking for a server at around the $100/month price point, this is worth seriously considering.

We have this knowledge base article on connecting an OVH server to GridPane:

Provision an OVH Server Using Our Custom Server Option

### ReliableSite

If you need a great dedicated server provider in North America, look no further than ReliableSite. They have an exceptional selection of servers for fantastic prices, and they have proven to be incredibly reliable – really living up to their name.

### Katapult

Katapult is a new, up-and-coming IaaS provider based out of the UK, with datacenters in London, and USA East and West Coast, with many more datacenters are planned. Not only do they offer excellent performance, but they are powered entirely by renewable energy, which very few other providers worldwide can say.

We ourselves at GridPane use Katapult for numerous projects and highly recommend them.

New accounts are offered $100 / £100 in free credits to get started. We have this knowledge base article on using Katapult with GridPane:

Provision a Katapult Server using our Custom Server Option

### Google Compute Cloud and AWS EC2

They both have outstanding networks and a great selection of datacentre options across the world, but they also charge a heavy premium, their pricing is confusing, and their UI is even more confusing.

For most websites, our native providers (except Lightsail) offer performance so good that you simply won’t notice the difference if you choose the datacentre closest to your target audiences.

That said, if you wanted to check out Google they offer $300 free credit for 12 months and their C2 offering has their higher performance CPUs.

We have these articles on using GCP and AWS EC2 with GridPane:

 

## Get Your Questions Answered

Do you still have further questions? Please post them over in the community forum and ourselves at GridPane and the community can assist you:

https://community.gridpane.com/

 

 

### Information

You may also be interested in this article which explores server sizing indepth: 
What Size Servers to Choose and When to Scale Servers Up

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

