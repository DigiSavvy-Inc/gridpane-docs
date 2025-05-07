# Floating IP Addresses and GridPane | GridPane

# Floating IP Addresses and GridPane

 

4 min read 

### Table of Contents

 

## Introduction

A floating IP address is an additional IP address that you can attach to one of your servers in a particular data center. The major benefit of these as a hosting/care provider is that you can also instantly switch floating IP addresses to a different server in the same data center.

They’re a few potential use cases where they can prove to be extremely useful and improve your internal workflow.

In this article, we’ll look at how to use them with your GridPane servers and a handful of scenarios where they can be implemented.

 

 

### Information

You may also be interested in combining floating IP addresses with our dns management with CNAME's strategy to improve your workflow: 
DNS Management Strategy and CNAME Flattening

## Floating IPs and Your GridPane Servers

By default, all of your servers come with an IP address that should be static (meaning that it will never change). This default static IP (NOT the floating IP) is the one that will be used inside your GridPane account and the one that you will see next to your server and the sites that live on it.

This will happen automatically when provisioning servers via API. When provisioning custom servers, always be sure to use the static IP that was automatically assigned and not the floating IP.

### Floating IPs are only for your websites

To make use of floating IPs, you can point your website/s DNS to this address instead of the static IP. Your sites will still work with your GridPane account. You could actually access your sites via both IP addresses with a local redirect.

### Overview

 

## Use Cases

Below we’ll look at four different use cases where a floating IP could come in handy:

### Scaling up/migrating with no downtime or DNS changes

This covers a few different scenarios: –

Here you would simply clone your site/s across with our cloning feature, and then when you’re ready, switch the floating IP over to the new server to set them live instantly. There would be no need to change each website’s DNS records manually.

### Website Relaunch

You have a big important project that’s been rebuilt and it’s living on a different server. When you’re ready to set it live, simply switch the floating IP from the older server to the new server, and your project will be instantly live to the world.

This typically only makes sense for larger-scale projects.

### SEO

From time to time, we get asked whether all websites can have their own IP addresses for SEO purposes. The answer is probably not unless you only host a small number of sites per server and your server provider allows for multiple floating IP addresses.

However, if you only have a handful of sites that require their own unique IP address, then floating IPs can help you accomplish this easily.

### You don’t control a website’s DNS

This ties into number 1 above, but it’s worthy of its own mention simply because when the time comes when you do need to move a site to a new server, no matter the reason, a floating IP address means you don’t need to go to your client and have the whole “please change your DNS records” conversation.

You simply clone the site, then switch the floating IP over and you’re done (assuming you use the same provider and the same data center, of course).

Check out this guide for more information on DNS strategy:DNS Management Strategy and CNAME Flattening

 

## IaaS Provider Guides

Below are links to the floating IP documentation on DigitalOcean, Vultr, and UpCloud. Linode appears to offer floating IP addresses on request (contact their support), and they are not available on Lightsail.

Please note that on UpCloud you will need to do some manual configuration.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

