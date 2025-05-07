# Getting Started with GridPane | GridPane

# Getting Started with GridPane

 

3 min read 

## Welcome to GridPane!

We’re glad that you are here! Our platform is very straightforward, but there are a few steps and requirements.

### Table of Contents

 

## Account Activation

Once you’ve registered for your account you need to confirm your email address to activate it. On signing up we’ll immediately send you an activation link – as soon as you click on it you can then start adding new servers and sites.

 

## Infrastructure: Connect Your Servers to GridPane

What you’ll need first is infrastructure! It’s BYOI here at GridPane. We natively support 5 of the most well-known providers (Core is currently only Vultr), and we also have a custom server option so you can choose servers from any high-quality provider worldwide.

All you need to do for our API integrations is sign up with one of these providers, get an API key, add it to your GridPane account, and spin the server up through our GridPane UI.

### Further Reading

To learn more about choosing and setting up your first servers, here’s our additional getting started article:

Getting Started: Choosing Your First Servers and Common Server Questions

Here’s the Provisioning Servers section of our knowledge base:

Provisioning Servers

 

## Creating and Managing Websites

Once you have a server set up, it’s time to add a site. In many cases, our customers are migrating a site into the GridPane platform, and there are a few things you might need depending on where you’re coming from. Here’s a guide to doing a zero-downtime migration:

How to Migrate to GridPane with Zero Downtime

Here at GridPane, we believe in using the very best tool for each part of a website. For example, if you’re coming from a cPanel/Plesk/DirectAdmin-based environment, you may be used to everything just being done for you. cPanel is a jack of all trades, master of none, so while it does a lot of things for you, it’s not the best. So here are the basics you’ll need:

 

### DNS Provider

If you’re coming from cPanel, typically DNS is handled by cPanel, so you’ll need a new DNS host. You can use the registrar of your domain (where you bought it), Cloudflare, or DNS Made Easy, just to name a few.

Cloudflare is strongly recommended, it’s free for DNS usage, and they are always at the tip of the spear when it comes to performance: https://www.dnsperf.com/. If you’re coming from Flywheel, Kinsta, WPEngine, Runcloud, Cloudways, etc, you’ll probably already have a DNS provider and be familiar with it. Here’s a beginners guide to DNS:

Setting DNS Records

 

### Email Provider

If you’re using Flywheel, Kinsta, WPEngine, Runcloud, Cloudways, etc, you’re probably already using an email provider like Office 365, GSuite, MXroute, etc. If you’re coming from a cPanel/Plesk/DirectAdmin provider, you might be using the built-in email, and you’ll need to find a new provider for your email hosting. Office 365 and GSuite are the top providers in this space. MXroute and Zoho are not bad.

In addition to sorting out email hosting, we also don’t install email on the server stack when you spin up a server. That means that when you add a site to your GridPane server, your site won’t automatically send emails (password reset emails, order emails, etc). You’re not left without options though, and we provide an integration with SendGrid to make things easier:

Using SendGrid SMTP for Transactional Emails

For other providers, we highly recommend the free Fluent SMTP plugin. This allows you to connect with all the main providers such as Postmark, AWS SES, Mailgun, SendinBlue, etc.

 

## You’re Ready to Go!

Once you have these 3 figured out:

This is really all you need to get started on the GridPane platform.

For more getting started docs, please check out the Getting Started section of our knowledge base.

Links to all of our platform feature documentation can be found here.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

