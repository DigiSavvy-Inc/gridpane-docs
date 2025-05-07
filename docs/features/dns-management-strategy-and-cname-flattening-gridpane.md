# DNS Management Strategy and CNAME Flattening | GridPane

# DNS Management Strategy and CNAME Flattening

 

7 min read 

### Table of Contents

 

## Introduction

As the hosting side of your business grows, having an effective DNS strategy can save you a great deal of time (and also tedious work). The strategic use of CNAME flattening can help streamline your DNS management.

This is also especially helpful if you’re hosting:

If you’re new to managing DNS, you may first want to check out our article on setting up DNS records:

Setting DNS Records.

 

## What is CNAME Flattening?

CNAME stands for “canonical name” and it’s used to map one domain to another. This is normally used so that only one A record requires updating anytime you make a server change that would affect multiple records such as “www”.

CNAME flattening (aka ANAME records) is where you use a CNAME for the root domain instead of a standard A record. This allows you to manage the IP address via another A record, which can be set at an entirely different domain.

 

 

### Information

Unfortunately, not all DNS providers will allow you to set the root domain up via a CNAME record. Cloudflare and DNS Made Easy both allow for this. Others, like GoDaddy for example (at the time of writing), only allow the root domain record to set as an A record. If the DNS provider you or your client is using does not allow for CNAMEs to be used on the root domain, this method will not work for you.

## How it Works

For our use case here in this article, instead of setting an A record for the root domain (e.g. yourclientsdomain.com), you would set up a CNAME and then point it to a custom subdomain record on a domain name you control.

You can then use this domain that you control to point to the IP of the appropriate GridPane server. Then, in the future, if you need to move this website to another server, you can update the IP address of the domain that you control, and your client’s websites will then also automatically point to this new server due to the CNAME.

### How this looks in practice

For example, if your client’s website was “gridpane.xyz“, you could set up their CNAMEs (including staging) as shown in the image below (this screenshot is from Cloudflare, but you can do this with any service that allows you to manage DNS records):

Then at yourdomain.com, you set the following A record for the subdomain “clientname.yourdomain.com“:

Now, gridpane.xyz, www.gridpane.xyz, and staging.gridpane.xyz all point to the IP address: 199.199.199.19.

In the future if you need to move this website to a new server and need to update this IP address, you will not need to touch their DNS directly, and you can simply update this A record at yourdomain.com.

Once your own A record is set and your clients (or whomever) records are set, you’re all set!

 

## CNAME Flattening + Floating IP Addresses

You can make your internal processes even more efficient by combining the use of CNAME flattening and floating IP addresses.

Floating IP addresses allow you to add additional IP addresses to your servers directly at your server provider. Then, instead of pointing the A record to the IP address shown in the GridPane dashboard, you point it to this floating IP address.

In practice, the server operates as if it has two IP addresses, so there will be no problem provisioning SSL records for your websites.

### The Benefit

As an example, let’s say we have a server that hosts 30 websites. One strategy could be to use CNAME flattening to point all 30 sites to the same subdomain record to manage their IP address. This way, when you move them to a new server down the line, you just update the one IP address.

That may be fine if all these websites are destined to live on the same server together for years to come, but what if one website grows in traffic, or it just makes sense to host them on a different server? Here it would have been more beneficial for this site to have its own individual record you can manage.

However, you could instead use a floating IP address to accomplish the exact same thing, and here you wouldn’t even need to touch DNS. Once you’ve cloned your websites to a new server, you just move the floating IP address from the old server to the new server and then all your sites are instantly served from the new server.

This means you get the same benefit, but you can still add individual subdomains for each client site when you first onboard them.

Now, if ever needed, you have the flexibility to update that singular IP address without ever needing to contact the client, and the rest of the sites on the server remain unaffected.

 

## Strategies in Practice

Below are a few different strategies and how they look in practice.

 

 

### Pro Tip

While you can use your own primary website domain, many GridPane power users register a separate domain and use it solely for DNS management purposes and our Cloudflare / DNS Made Easy integration.

### Strategy 1: CNAME Flattening Only

In practice, this requires two steps – assuming you’re making these changes when you’re ready to set the website live on GridPane server:

Once the DNS changes propagate, their website will then be live on your GridPane server.

 

### Strategy 2: CNAME Flattening + Floating IP Addresses

This strategy is essentially the same as strategy 1 above, with two key differences:

Once this is done, you can then start following the client onboarding steps.

In the future, you can either use the floating IP address to move a website to a different server (when all sites on a given server are being migrated) or change you can update their A record if they’re moving but the other sites are staying put. Our article on floating IP addresses can be viewed here:

Floating IP Addresses and GridPane

 

### Strategy 3: Include DNS API Proxy Records

Follow either strategy 1 or 2 above, but also set up DNS API proxy CNAME records. Setting these up on client sites where you don’t control their DNS inside of your Cloudflare or DNS Made Easy account means that you will always be able to provision SSL records for these websites without needing the DNS to be live in advance. Full details can be found here:

Provisioning an SSL for a domain using DNS API Domain verification by Proxy Challenge

This is how those records would look inside the client’s DNS account (like the examples above, the client is gridpane.xyz):

 

### WaaS Network Strategy

WaaS networks are generally much more hands-off than regular hosting and care plans. Here, floating IP addresses are an excellent choice, and if your clients are following documentation you’ve created and configuring their own DNS, it may be easier to just have them all point to the same record instead of setting up individual records for each site.

This strategy is particularly powerful as you could host hundreds of sites on one server (not recommended) but easily move them all to another and then simply move the floating IP address over or change just one A record and you’re done.

 

 

### Final Note

Pointing CNAME records towards a domain behind Cloudflare's proxy has worked perfectly fine in our testing.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

