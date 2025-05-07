# GridPane Features Update - What We’re Working On, Future Plans | GridPane

# GridPane Features Update – What We’re Working On, Future Plans

 

9 min read 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='673'%20viewBox='0%200%201024%20673'%3E%3C/svg%3E)

It’s been some time since we released a big update on what we’re working on behind the scenes. Below, we’ll cover a lot of the most asked questions we’ve been getting, including an update on each of the individual Developer Plus features and what’s coming.

### Table of Contents

 

## PanelPress V2

Version 2 of PanelPress has hit some roadblocks. These have pushed our internal timeline back considerably.

The future plan is for WPaaS, where WP.Cloud lives, and PanelPress to live together within one master Panel, and it will be a significant upgrade to V1.

A lot of time, energy, and money is being invested in PanelPress, but it will take as long as it takes, and we will send updates when the time comes. Right now, we don’t have a launch ETA.

 

## Developer LTD/Monthly/Annual

We’ve been asked about what’s going on with Developer legacy. Here’s what’s currently in the works:

1 and 2 are actively being developed/re-developed, and we’ll have a specific update on UpdateSafely soon – this is right at the top of our priority list.

We’re constantly developing the foundations of the platform, and that includes the recent release of Ubuntu 22.04 and the myriad of long-term improvements this has brought. Developer Legacy will continue to benefit tremendously from our continued efforts and support.

 

## Developer PLUS Features

### 1. Fortress UI Integration

Fortress will soon be available directly within the UI, inside the website customizer security tab. Functionality will include:

This will make getting started and general troubleshooting a lot easier. Additional licenses will also be available to purchase as an addon within the UI.

 

### 2. Uptime Monitoring

This is on its way and will include all your production sites. It will not be limited to 50 sites as we originally planned. The bulk of the work has already been done, and it will soon be available to turn on via a toggle in the site customizer.

 

### 3. DNS Failover for 50 Sites

Managed failover requires Snapshot Failover and one of the following:

… and is available now. Contact us to get details on how best to activate this functionality based on your unique DNS provider.

 

### 4. Vulnerability Monitoring

This is available for ALL of your sites, not just the 50 sites we’d included at launch. The vulnerability scanner has also just undergone a huge under-the-hood upgrade today, improving performance and stability. Learn more here: WordPress Vulnerability Scanning and Notifications

 

### 5. Vulnerability Remediation

After extensive testing of different automated solutions for applying updates – whether they patch known security vulnerabilities or if they’re simply new feature updates – it’s become clear to us that the only consistently SAFE way to do that is to always have a human being in the loop AND to have a clearly defined playbook for handling vulnerabilities based on the severity of the threat and the exact remediation pathways available.

Which is why we’ve decided that for all the sites previously sold under the coverage of “Scanning and Patching” will now have our highest tier of per-site support with 360, our truly managed white-glove support option used most commonly by our higher-tier Agency clients.

With 360, not only will you get proactive remediation of security vulnerabilities but you’ll have constant 24/7 monitoring by our team of all of your most critical applications and servers. All sites and servers enrolled in 360 get a thorough health check, a tenancy/resource assessment, and they’re connected to our team’s monitoring systems for resolution of issues while you sleep.

In the future, as we ship our completed overhaul of UpdateSafely, you’ll be able to extend a form of “remediation” across all of your websites by simply choosing to have some or all of core, theme, and plugin updates be applied automatically, after passing visual regression testing.

#### Important: Specific requirements of sites covered by 360

All sites approved for 360 support have a comprehensive health check of the entire server and all applications on it.

No sites on a 360-supported server can be excluded from 360 coverage. Meaning when you enroll a server into 360 every site on that box is covered by 360.

You can run 50 sites on 50 different servers, all of them will be covered by 360, and that would keep you within your 50-site limit without any additional expense.

However, if you have a staging or development site on a server covered by 360, those sites will also be counted towards your total, as they cannot be excluded from our monitoring and support.

Ideally, you would perform staging and development work on servers dedicated to that specific purpose and not mix staging environments with production environments.

 

### 6. Object Cache Pro & Relay Integration for 1 Website (Minimum $242/month value)

This feature is being expanded and will now be called Dynamic Enterprise Applications.

There have been some pain points rolling this out in a manner that makes it easy to turn on and off. However, this is close to completion, and we now have:

These Dynamic Enterprise sites also include a one-time site audit and infrastructure recommendations. Additional licenses, load balancing, and multi-CDN upgrades will be available in the future).

 

### 7. 50 Additional PanelPress Sites

All Developer Plus accounts do come with 50 additional websites (plus the 10 included in Developer Legacy for a total of 60), all of which can be assigned to separate clients.

 

### Upgrade Addition 1: Multitenancy

We’ve added multitenancy into Developer Plus, which was previously only available at our Agency tier. This is already available for everyone.

Multitenancy can be a game changer for both security and simplifying the management of your websites. Benefits include:

You can learn more about multitenancy here:

 

### Upgrade Addition 2: BitNinja ($144/month value+)

We’ve struck a deal with BitNinja, and Developer Plus will include its use on up to 3 servers (with more available as an addon). These servers will not be limited by the regular BitNinja system user policy and will be available for ALL system users (and, therefore ALL sites) on your servers.

BitNinja includes:

 

### Upgrade Addition 3: Development Domains and Development Environments

After years of requests, usually from people who don’t quite understand our mindset around deploying development environments, we’ve decided to add “development domains” to GridPane. What does this mean? It means that when building new sites, you’ll be able to auto-generate a random subdomain for a site without needing to create your own subdomains and DNS records.

Also, we’re including 50 development environments for all Dev PLUS accounts. Development environments are WordPress applications that you can build in your account, which include free access to our best available tools (like OCP, Relay, and Fortress) on a development subdomain of your choosing.

You’ll have the option of “bringing your own” or using a domain that we’ll purchase for you, included free within your paid account. (TLD restrictions apply, and we’ve already got some pretty… noteworthy domains available for your choosing).

A simple example of what this will look like:

Note: you can continue to do all of this in the traditional “GridPane fashion” and just add your domains and subdomains of new projects just as you’ve always done. This auto-generate option will speed things along a bit, and it’ll include premium security and performance options for your most important projects.

Look for more details on the Development Domains/Environments rollout in December.

 

## PeakFreq

And finally, PeakFreq is, of course, live and kicking. This is available to ALL GridPane account holders, including our free Core account.

This is a service/feature that we couldn’t pass up. Not only because of the Cloudways acquisition by DigitalOcean and the unique opportunity this presented but also because we’ve long needed a quick start button for the 1000s of people who look at our platform and assume it’s too complicated for them.

PeakFreq makes getting started with our platform as simple as signing up and adding billing information. There’s no need to sign up to an additional server provider company, add billing info, create an API key, and then take this back to GridPane. It also helps reduce the fear that so many have when they first start going the VPS hosting route for their business – a decision that we all know is the right call for almost all WordPress professionals.

And so here we are. PeakFreq is a fully functional, less expensive, more performant, and an all-around excellent alternative to Cloudways.

 

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

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

 

 