# Scaling Your WaaS Network: Advice for WP Ultimo, and Multisite vs Multitenancy | GridPane

# Scaling Your WaaS Network: Advice for WP Ultimo, and Multisite vs Multitenancy

 

9 min read 

## Introduction

WaaS networks are a popular revenue channel for more WordPress professionals and agencies. They allow for a relatively hands-off, predictable monthly revenue stream where clients handle most of their own website building using premade templates.

For now, WP-Ultimo is really the only plugin available for a multisite WaaS. We have an integration with Ultimo that will add mapped domains to the domains tab inside your website’s customizer, and you can use our AutoSSL feature to automatically attempt to provision an SSL for these domains as they’re added.

Ultimo is a great plugin for market validation and proving that you have a business that you can grow. To build a truly scalable WordPress SaaS though, multitenancy is the only safe, secure, limitation-free solution.

### Table of Contents

 

## Multisite vs Multitenancy

WordPress multisite is a single installation of WordPress where network sites exist as subsites within this single installation. It has one shared database, one system user, and all the sites live together sharing the same resources.

Multitenancy is a solution to the problems that come built-in with multisite/WaaS networks. Unlike multisite, multitenancy shares the same WordPress codebase, but each site within the network has its own PHP user and its own database, keeping them independent from one another.

The WordPress codebase that each site runs off is immutable, making multitenancy sites more secure than even regular WordPress sites, and far more secure than regular multisites. Updates to the WordPress codebase are made via GIT and go out instantly across the network.

This approach allows sites to be split across as many servers as needed, spreading “risk” across many baskets instead of everything being on the same server, same database. You can even add sites to their own individual servers, which means multitenancy also works for WooCommerce and other complex websites which can be a disaster when running inside one multisite installation.

It’s the only way to scale a WaaS network in a safe and secure way.

### Summary

At GridPane, multitenancy is available on our Developer Plus and Agency plans.

 

## Multisite Network Management Strategy and Scaling Problems

In the early days of your WaaS when running a multisite installation, one of the best things you can do minimize your risks is to cap your network size and use multiple installations.

This way you can have multiple networks running on multiple servers, which in turn keeps your database size more manageable, keeps your networks more mobile (meaning it’s much easier to move a small 2-3GB multisite than it is a 30GB multisite), potentially keeps them more secure, and it means that you’re not putting all your eggs in the same basket. If you have a giant network, if you ever have a situation where ALL of your sites go down at the same time, you’re going to have a hell of a day in support.

There are a couple of ways to do this, and it will affect your sign-up workflow.

### Option 1. Rotate your network out once it reaches X number of sites

Here you would have a primary marketing site, and then when your customers go to sign up they would click through to your multisite which would be its own separate site. Once you reach X number of sites, simply swap the network out for a new one on a new server.

So for example you may have:

And so on. Your primary marketing site links through to the separate network sites which is where they sign up, and you just switch the link out on the marketing site when you switch your network out.

### Option 2. Use Different Locations

This option is largely the same as option 1 above, except on your marketing site you offer a choice of locations. For example, you may have a network option in LA, New York, and London:

When your customers select their location they click through to the applicable network.

You can then switch these networks out as they reach X number of sites, and have la2, ny2, uk2, etc.

 

## DNS Management, CNAMEs, and Floating IPs

At some point, you’ll need to move your WaaS network from one server to another. This may be because the OS has reached its end of life or your changing infrastructure providers, but whatever the reason, it will be necessary.

For some network owners, this may mean having to reach out to every single site owner in their network and asking them to update their DNS records. Ideally, you want to avoid ever having to do this, especially as you grow. Here are two strategies to consider.

### 1. Take Advantage of Floating IP Addresses

If you’re following the guidance above and using multiple networks and keeping them relatively small in size, then as long as you stick with the same provider you can take advantage of floating IPs.

When you provision your server, you’ll be assigned a static IP (e.g. 123.123.123.10). You can then assign a floating IP address to this server (e.g. 199.199.199.19). This will make the sites on your server available on both of these IPs, so you can specifically have your clients set their A and CNAME records to point to the floating IP (in this example, 199.199.199.19).

When the time comes to move servers, simply clone your network across, check and ensure it’s been cloned successfully, and then when ready, switch your floating IP over to the new server. Neither you nor your clients will need to update your DNS records.

You can learn more about floating IPs in this article: Floating IP Addresses and GridPane

### 2. Have Your Clients Use CNAMEs

Instead of having your clients set the traditional A record for the root domain and CNAME record for “www”, have your clients instead set both of these up as CNAMEs and point them to a domain that you control.

You can then use this domain that you control to point to the IP of the appropriate GridPane server. Then, in the future, if/when you need to move this website to another server, you can update the IP address of the domain that you control, and your client’s websites will then also automatically point to this new server due to the CNAME.

You won’t ever need to touch their DNS directly, but this way you can control what IP all of the websites are pointing to.

### Take Control of Client’s DNS Wherever Possible

The most ideal path for you as the network owner would be to have your clients let you take control over DNS with either Cloudflare or DNS Made Easy.

This way you can ensure that either one or both of the above strategies are in place, and once they’re set up, you don’t need to worry about changing these records ever again.

 

## SMTP

The easiest approach to SMTP is to simply send all transactional emails from the main network domain. This is what will happen out of the box once mail has been set up. It’s not only easier to set up, but it will prevent support issues related to email deliverability where clients haven’t set up their SPF records and validated their domain.

If you need for mail to be sent from each individual subsites domain then this is a little trickier. The official SendGrid plugin used to offer this functionality, however, unfortunately, it has not been maintained and we don’t recommend using it for this reason.

A good alternative that can help you accomplish this is the 100% free FluentSMTP plugin. It requires that this be set up for each individual subsite, so you may want to provide training for your network sign-ups on how to do this.

 

## Performance

Performance advice here is different for multitenancy and multisite, and this is largely due to all the limitations/drawbacks that come with multisites.

### Multitenancy Performance

Multitenancy performance is straightforward. There’s very little difference to managing regular domains, so you can give each individual site the resources they need, you can host them on their own servers if you want to, and scale those servers up as these sites grow.

All the standard advice applies – use higher frequency CPUs, fast RAM, fast storage, etc. You can also tune your PHP workers on a per-site basis, as well as all your other PHP settings. Getting high performance out of your sites isn’t as complicated as most people think. Check out this guide for more information:

WordPress Performance: Common Questions and Answers

### Multisite Performance

For your multisite, you should approach it like you would a large dynamic site (like a Woo store or an LMS).

If you keep your networks small (30 sites is a good number in my opinion), they likely won’t require more than a 2 CPU 4GB RAM server. We recommend Vultr High Frequency, but DigitalOceans Premium AMD Droplets and Vultr’s newer High-Performance options are all also good choices.

Higher performance CPUs will help keep your backend admin area snappy and fast and provide a better editing experience for both you and your customers.

If your current network is slow, here is a good place to start:

Why is my WaaS network slow? Table locking and MySQL RAM allocation

 

## Further Reading

Below are links to all of the articles mentioned in this guide:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

