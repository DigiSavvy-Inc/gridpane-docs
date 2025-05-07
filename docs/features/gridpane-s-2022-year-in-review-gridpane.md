# GridPane’s 2022 Year in Review | GridPane

14 min read 

# GridPane's 2022 Year in Review

 

### Table of Contents

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='673'%20viewBox='0%200%201024%20673'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2023/01/GridPane-2022-Year-in-Review-1-1024x673.jpg) 

## Intro & Happy New Year!

Hey WordPress Warriors! We hope you enjoyed the holidays and were able to get some downtime, and we wish you all the best for 2023.

2022 was another interesting and eventful year. Lots of updates, refactoring and improvements, new features, and more. We’ll take a look at the highlights below.

### The Business

From the release of our FREE Core plan to Automattic investing in GridPane, it’s been an eventful year on the business side of the equation. We’ve grown way beyond 100,000 WordPress sites, and we continue to host more every single day.

### The Platform

A lot of the work that goes on behind the scenes here at GridPane slips by under the radar. However, this is the work that makes our platform what it is – one of, if not the most, reliable, customizable, and performant WordPress hosting platforms in the world for even the most demanding sites.

Literally hundreds of thousands of lines of code were added or edited throughout 2022, improving and/or maintaining our stacks and platform.

 

## Automattic Invests in GridPane

Just before WCUS on September 7th, we announced the completion of a seed round of funding that included a significant strategic investment from Automattic, the parent company of WordPress.com, WooCommerce, WordPress VIP, and Jetpack.

This was pretty big news for us, and chances are pretty high that you’ve already read our announcement blog post, but if you haven’t, I’d highly recommend that you check it out here:

Self-Managed WordPress Pioneer GridPane Takes Strategic Investment from Automattic

 

## GridPane Plans

### Launch of the Free Core Plan

Much to Patrick’s amusement, we launched our free Core plan on April 1st. While its feature set is limited compared to our paid plans, Core includes all the performance and caching benefits of those plans. It’s perfect for anyone just getting started in offering their own hosting service and/or allows busy sites with a small budget to use our software completely free and gain incredible performance for the direct cost of their server.

### The launch of Developer PLUS

Our Developer plan features are now only available as Developer Plus along with additional third-party software and services. These additional services make this plan a major upgrade to most fully managed WordPress hosting services and will have a massive impact for developers and agencies offering their own hosting services. ### A refocused Enterprise Plan

Enterprise is specifically for hosting companies (existing or soon to be), who want all the capabilities of our platform to use as the foundation of their business. For any hosting company looking to move away from cPanel, GridPane Enterprise is the solution.

 

## Affiliate Program Relaunch

The long-awaited relaunch of our affiliate program went live in October and has, of course, been updated along with our plan increases.

We believe this is one of, if not the most, competitive hosting affiliate programs on the market, with up to $1500 commissions and monthly recurring commissions for Panel and Developer Plus plan referrals.

Full details and a link to sign up can be found here: The GridPane Affiliate Program

NOTE: To be eligible to sign up, you will need to be on a paid GridPane plan and have made your first payment once the free trial period has ended. A verification check will automatically take place during the sign-up process, so there’s no need to wait on us to manually approve your account.

 

## The GridPane Client Portal: PanelPress.io

The Client Portal was released into open beta in May. This was a HUGE release for us and one that we hope will have a significant impact for you and your business – especially if you’re looking to grow the hosting and recurring revenue side of your business this coming year.

The 2nd iteration is already well underway, and we’re very excited about what 2023 holds for you and the WordPress hosting industry as a whole.

You can learn more about PanelPress.io and its releases in this intro blog post:

Officially Introducing PanelPress.io: The New GridPane Client Portal

 

## Managed Hosting and WP.cloud

We became the first host outside of Automattic who have integration with wp.cloud – Automattic’s scalable, highly available, extremely fast WordPress cloud platform.

In September, we started our WP Cloud integration with GridPane. This is a highly custom environment, so its availability and integration will differ significantly from our other server provider integrations.

If you have a highly demanding website, such as a big and busy WooCommerce store, high concurrency LMS and/or Buddyboss, etc, then WP Cloud may be an ideal solution for you.

This compliments our existing Apollo fully managed hosting service, which has also received numerous upgrades in terms of massive scalability and also database performance with OCP and relay.

 

## Ubuntu 20.04 Stacks (x3)

The much anticipated Ubuntu 20.04 release was released in April and includes 2 new stacks for Nginx and one new stack for OpenLiteSpeed:

This release was a herculean effort from our team and was originally delayed due to the lack of support for Nginx and HTTP/3. We ended up rolling out our own as a third option.

We began work for our 22.04 releases in Q4, and these will launch in 2023.

 

## The GridPane Git Integration

Our Git integration first went live in June, and this was another major release and a milestone feature. It includes two different Git integrations options for different use cases:

### Full Repositories

Our full integration is what most users will be familiar with, and with this, WordPress core, plugins, and themes are all managed via Git. The entire codebase is immutable, and so WordPress updates can only be done via Git deployments.

### Hybrid Repositories

Our hybrid integration is for those of you who only want to handle specific plugins and themes via Git. Unlike the full repo as described above, the hybrid repo is not immutable, so WordPress core and any other themes and plugins not set in your repo are handled the traditional way inside the WordPress dashboard.

### Pre and Post Deployment Scripts

It also allows for scripts to be run as root and/or the website’s system user both before the deployment and/or after the deployment.

Links to more information can be found here.

 

## Multitenancy Relaunch

In conjunction with the new Git features, our multitenancy solution was updated to take advantage of the same scripts and feature integrations.

Multitenancy now uses the same Full Git Repository as standard Gridane Full Git Integration, and there’s a significant amount of crossover between how the two features work.

This was a significant update that made the feature set a lot more accessible in terms of usability and making the most out of the entire suite of GridPane tools.

Multitenancy is available on Agency Plan.

 

## Nginoil

Nginoil is a very cool, optional feature that runs as a part of the nginx.service when it starts up. This didn’t receive a ton of attention, but it’s definitely a feature that you should revisit in the near future if you’re not already taking advantage of it.

Unlike a regular start-up that runs a standard nginx -t, Nginoil has built-in functionality to detect where Nginx syntax errors are originating from and implement a fix that allows Nginx to boot up successfully. It can be activated via GP-CLI, or there’s also a toggle in the Server Customizer > Nginx tab, so you can easily activate/deactivate this directly inside your GridPane dashboard.

GridPane Nginoil – Automatically Fix Nginx Syntax Errors

Along with Nginoil came some updates to our gp nginx -t and gp nginx reload commands. Details are also in the above article.

 

## Continued Development of the API

New endpoints have rolled out throughout the year, and while it is still technically in beta, this is essentially due to the fact that it is still being developed. We ourselves are the biggest user of the API, and it is actively tested and used in many people’s production workflow.

Work on the process manager is well underway, with a significant amount of ground covered in Q4 2022. Once rolled out, it will prevent the potential for server overload, and we’ll be able to ease the restrictions on the Developer and Developer PLUS plans. We look forward to its role out in 2023.

 

## Platform Improvements

This includes iterations across our entire code base to make things reliable and performant as possible for even the most demanding sites, and also as easy as possible to customize both our Nginx and OpenLiteSpeed stacks. Improvements to overall workflow have also been added throughout the course of the year, such as database rewrite options and V2 backup restore options.

We host servers with crazy customizations, sites that generate millions of dollars, and sites that other hosts can’t even handle. Building in reliability is of paramount importance, and a great deal of work takes place in the background to make GridPane as bulletproof as possible.

Some of the other additional improvements include database rewrite options, rewrite fallbacks, new guards, new V2 backup restore options, new GP-CLI, iterations to our security measures, PHP 8.1, major speed upgrades to the dashboard, and more.

 

## The Knowledge Base and Blog

As per usual, there was a lot of new content published over the course of 2022. This includes both the knowledge base and the blog.

#### Fast stats:

We published 51 new knowledge base articles throughout last year, and we now have a total of 355 published articles, along with 4 learning paths.

The entire knowledge base was reorganized and re-categorized to make finding content easier and more intuitive.

We also re-arranged the main knowledge base page, adding a quick reference section for all the platform-specific documentation, and we’ve added a new learning path. The troubleshooting documentation has also all been collected into one quick reference page, which can be seen highlighted with a red border.

With so many articles also comes a great deal of maintenance, and a vast amount of time went into improving and/or updating the existing articles.

Below are some of the content highlights from last year.

 

 

## Content Highlights

 

Below is a selection of our most popular content from 2022.

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2022/04/WordPress-Cloudflare-Firewall-Rules.jpg) 

### Cloudflare Firewall Rules for Securing WordPress Websites

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='673'%20viewBox='0%200%201024%20673'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2020/06/WordPress-Knowledge-Base-1024x673.jpg) 

### How and Why We Built Our Knowledge Base on WordPress

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2023/01/GridPane-Git-Documentation.jpg) 

### Git: All the Docs

 

Read Documentation

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2022/09/WaaS-Performance.jpg) 

### Scaling Your WaaS Network: Advice for WP Ultimo, and Multisite vs Multitenancy

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2022/06/Stop-Comment-Spam.jpg) 

### How to Stop WordPress Comment Spam Permanently (for FREE)

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2022/06/Eric-Jones-Spam.jpg) 

### How to Reduce Eric Jones Spam (and all the other Contact Form Spam)

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2022/05/Mitigating-a-DoS-DDoS-Attack-WordPRess.jpg) 

### Mitigating DoS and DDoS Attacks On Your WordPress Websites

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2022/06/Block-Bad-Bots.jpg) 

### How to Block Bad Bots from Your Sites/Servers

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2022/09/WordPress-Performance-QA.jpg) 

### WordPress Performance: Common Questions and Answers

 

Read Article

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2023/01/Create-a-Blueprint-Website.jpg) 

### Creating a Blueprint (AKA Boilerplate) WordPress Website to Speed Up Development

 

Read Article

 

 

## Patrick’s 2023 Predictions

Inspired by Kyle from the Admin Bar I’ve decided to put together a random smattering of predictions for 2023.

I feel like everything we accomplished this year speaks for itself. I continue to be utterly humbled by every single person on my team and everything that they do, day in and day out.

I’m looking forward to 2023. I’ve never been as excited about GP and this community as I am right now. And it only grows every single day.

So, without further delay, my 2023 predictions, in no particular order:

So get TF after it.

 

## Final Thoughts and Thanks

 

A huge thank you to all our team – especially our team members in Ukraine – for the amazing work they do day in and day out, and for making 2022 another amazing year for the GridPane community.

We hope you and yours have an amazing 2023!

 

 