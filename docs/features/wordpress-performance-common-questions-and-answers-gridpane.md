# WordPress Performance: Common Questions and Answers | GridPane

# WordPress Performance: Common Questions and Answers

 

11 min read 

## Introduction

The contents of this article started from a post in our Facebook group with some misunderstandings there are when it comes to “tuning” your server settings for performance.

That post resulted in this post in our Community Forum, and this article is essentially the contents of that post made public.

### Table of Contents

 

## Improving Performance at a Managed Host vs GridPane

Some context that I believe will be helpful here is the options that are available to you at a traditional “managed” WordPress host vs GridPane.

In the context of improving your WordPress sites performance at the server level, at a managed host you can:

That is all.

Their stack is already built for WordPress. They offer server-level caching, and maybe even Redis object caching if you’re lucky (and pay an additional $100/month per site).

So if caching is already turned on, and your website is having performance issues, you can either optimize your WordPress codebase and/or you can pay for more resources. Those are the options you have available to you.

 

## Improving Performance at GridPane

GridPane also offers WordPress optimized server-level stacks. They will work great out of the box for 95% of all websites.

The difference where I think most people go wrong on our platform is that you have so much control, and so many more options available to you compared to essentially any other host, and by a huge margin.

And with so many settings, what should you focus on to improve performance?

There are 2 main things on GridPane you should pay attention to:

That’s really all there is to it for 99% of everyone’s websites in terms of “tuning” your server-level settings.

On OpenLiteSpeed it’s even easier – just leave the default PHP LSAPI settings as they are by default.

#### Bonus Points:

 

## Learning More About Caching and Workers

For Nginx servers, you can learn more about whether you should use Redis page caching or FastCGI caching in their respective articles below. The really short version is that if you have very high concurrent traffic, then FastCGI will handle high concurrent load better than Redis will.

Also, if a site is publishing a lot of content regularly but clients are complaining their changes aren’t showing up on the live site, switching to FastCGI will save both of you some headaches – more details in the KBs:

To learn more about PHP FPM, check out this blog post:

If you really want to dig deeper into this, you can also check out these two articles from Pagely and Tideways to really hammer it all home:

 

## Further Performance Improvements

Your server settings are 1 of 3 ways to improve your website’s performance. The other two are:

Here we have the other two options that are available to you at managed hosts. Run a leaner codebase so your website runs more efficiently and requires fewer server resources, or increase your server resources. Or both.

GridPane has error logs, a one-click install of the query monitor plugin, and activation of wp_debug (which is then available directly in the UI), PHP slow logging, and MySQL slow logging. All of these tools can help you uncover where your codebase bottlenecks are, and once you know that, you can set about fixing them.

You can also use a server with a faster CPU and higher frequency RAM, and more of both of those.

#### Bonus Points:

OK, technically there is a 4th option that will reduce server overhead, and that’s using a service like Cloudflare or a CDN. These services will both improve your speed around the globe (in most cases), and reduce the amount of work your server has to do to serve your websites to your visitors. How much benefit you’ll actually gain depends on the type of website you’re running.

 

## Questions and Answers

#### What about load balancers?

If you’re not sure if you need a load balancer, then you don’t need a load balancer. If you’re not maxing out at least a dedicated server with 32 high-frequency cores (gaming servers ideally), then you’re not at the point where you need a load balancer, and using one would cost you a lot more in time, effort, complexity, and maintenance, and likely also money, than just using a bigger server would cost you.

#### What about troubleshooting and diagnosing server performance?

From a server optimization perspective, all the info you need is above.

Most of the time when people are talking about improving performance what they’re really talking about is fixing 502/504 issues which in 95% of cases are the result of codebase issues, and tweaking server settings really isn’t going to help, or at best will act as a bandaid to keep it limping along. The remaining 5% is usually that you just need a bigger server

For troubleshooting, you need to be able to identify which site on a server is causing the load (check top and htop to identify which websites are the most active), and then determine whether this is a legitimate rush of traffic, an attack, or just long-running requests due to a plugin locking up the database or serious PHP inefficiencies.

Each of these requires a different resolution.

For this, these two guides cover what I believe everyone on GridPane should take the time to learn:

#### How do I differentiate between a caching issue, vs memory issue, vs CPU issue, vs PHP-FPM issue?

```
[03-Dec-2021 01:59:02] WARNING: [pool examplewebsite.com74] seems busy (you may need to increase pm.start_servers, or pm.min/max_spare_servers), spawning 16 children, there are 0 idle, and 5 total children
```

If yes, you likely need additional CPUs to cope with the current workload. See the above articles for more details.

#### PHP Memory vs WordPress Memory and how they impact performance

WP_MEMORY_LIMIT is the memory limit WordPress sets at runtime for any given request. For practical purposes, you really only need to focus on your PHP INI settings within your GP dashboard. Our defaults are ideal. Allocating more memory may be necessary if your codebase has inefficiencies – sometimes this is just unavoidable depending on the site and client budget, but we’ve also seen sites that require 2GB of RAM just to save a page, and that’s some crazy shit.

If a site needs a ton of memory to operate, then PHP will potentially consume a ton of RAM, which could impact your overall performance by taking away RAM from other services that need it.

Your codebase is really what needs focusing on.

#### How to troubleshoot high CPU usage, and interpret htop and other command-line tools to say, “Okay, this site needs X, Y, or Z”

This is more of a misunderstanding than anything else. htop and top can help you identify what service is using the most CPU (PHP, MySQL, Nginx), it can help you identify a specific site that’s responsible for CPU usage, and it can help you identify things like iowait and CPU steal, which can both cause performance issues. You could also find that say backups are running and consuming a lot of resources for short periods of time.

It’s a starting point to help narrow down the source of your issues, and from there troubleshoot accordingly.

### Recommendations for Different Scenarios

In the Facebook post that started this, one of our clients outlined a few different scenarios.

### Scenario 1.

I have 50-60 brochureware sites, all are low-traffic. The best server for this is a 2vCPU cloud server with 4GB RAM, and caching enabled for all of them.

As a general rule of thumb, yes you should always cache everything, but this is probably too many sites for that small of a server unless they really are tiny in size. 10 sites per 1GB of RAM is probably the maximum you should go for – so a max of 40 sites on a server this size. Personally, I’d go with up to 30.

As an additional note, I also like the 2 vCPU 4GB RAM server size for hosting brochure sites. The value at this price range is excellent, that extra CPU can make a huge difference, and you can split your eggs between multiple baskets. I wouldn’t personally go above 4 CPUs for my servers hosting brochure sites.

### Scenario 2.

I have a high-volume online community-based site that gets a massive influx of traffic every morning for 2 hours. Caching doesn’t work well due to the nature of it being an online community, but the server needs to have enough resources to handle a lot of traffic at once. In this case, I am using a 4 vCPU High-Frequency server (8 GB RAM) with all caching disabled, but struggle constantly with what the PHP-FPM settings should be.

Here I’d turn on Redis object caching to reduce the burden on MySQL, which can be incredibly CPU intensive for these types of sites. I’d also try to cache whatever I could for any pages people hit when they’re not logged in – every little helps. If it’s just the one site on the server I’d set workers to static, and set the PM Max Children to 3 per vCPU to begin with (so 12 in total). From there it’s really just watching and seeing how it goes? Does the server never go past 80% CPU? If that’s true, additional CPU workers may help you take advantage of that extra 20%.

### Scenario 3.

I have a school district where 1000 computers turn on all within 10 minutes of each other and all load the district’s website upon boot. I ended up upgrading this cloud server from 2 vCPUs to 4vCPUs and turning FastCGI and Redis Object caching on, but again I struggle with the correct settings in PHP-FPM for this kind of site/traffic/load.

I have a few different thoughts that may be helpful. The issue sounds like it’s self-imposed, and unless they were willing to pay extra for what is a self-made problem, I’d first try switching to FastCGI + Redis Object Caching. I’d probably also set the TTL to 10 mins (600 seconds).

While you won’t notice a difference in page speed between the cache types on most websites, FastCGI handles concurrent load better than Redis, so you’ll get better performance when the site gets slammed in the morning.

A second, maybe better option, would be to create a very simple /welcome page for each subsite that’s just a few kb in size (SVG logo, any CSS straight in the HTML), and have it be the logo, and a link that just says “Enter Website” (or something like this). Have them load that page instead of the homepage when they boot up. You could also take advantage of something like Cloudflare here too if you’re not already.

For PHP FPM, if it’s the only site on the server I’d set the workers to static at 4 workers per vCPU (so in this case 16 PM Max Children in total). On OLS, I’d leave the default PHP LSAPI Processgroup settings.

 

## Do You Have a Question?

If you have a question you’d like answered that isn’t included here in this post, please feel free to ask it over on this community post in the forum and we’ll get back to you and update this article accordingly.

Community Forum: WordPress Performance Q&A

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

