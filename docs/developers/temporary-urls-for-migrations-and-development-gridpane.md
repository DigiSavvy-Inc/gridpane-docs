# Temporary URLs for Migrations and Development | GridPane

# Temporary URLs for Migrations and Development

 

2 min read 

### Table of Contents

 

## Introduction

A common question we get asked when many users first get started on the platform is “Does GridPane provide temporary URLs?”. The short is no we don’t, but you also don’t need them.

Many hosts do offer these, however, the URLs used often look bizarre and even untrustworthy, and contain a company name that your client has likely never even heard of.

Why use a hosting companies domain when you can instead use your own brand (or even your clients brand) for this very simple need?

With GridPane you have full control over this, and the workflow is almost exactly the same, with one exception: You choose exactly what your temporary URL will be when you create the site inside of your account.

Provisioning an SSL certificate is also quick and simple when using your own domain when it’s connected to Cloudflare or DNS Made Easy and using our API integration (more info in the further reading section).

Below are the three main methods members of the GridPane community use.

 

## Option 1. Use a Subdomain of Your Business Website

What most of our community do is simply use their own domain for migrations and development sites. This is would normally be:

clientname.yourdomain.com

If you’re using our Cloudflare or DNS Made Easy integrations (which we highly recommend), then our platform will automatically add your DNS records for you as long as they don’t already exist.

 

## Option 2. Use a Dedicated Development Domain

Another popular choice is use a dedicated domain that’s purely for development and migration purposes. It’s your own custom temporary domain, and it’s usually again something like:

clientname.yourbrand.dev

Add it to Cloudflare and use our API integration.

 

 

### Bonus

As an extra bonus, a dev domain is perfect to use as your Cloudflare or DNS Made Easy challenge domain for provisioning SSL certificates before setting the DNS live when you're not managing a client's DNS. Learn more here:

Provisioning an SSL for a domain using DNS API Domain verification by Proxy Challenge

## Option 3. Use a Subdomain of Your Client’s Domain

Finally, you could also use a subdomain of your client’s actual domain. This is generally less convenient than the first two options above, but there are sometimes situations where this can make sense (for example, if you’re building a site on a white label basis).

 

## Further Reading

Using our Cloudflare or DNS Made Easy integrations make using your own custom temporary URLs a breeze. For more information on using these services with GridPane, please check out the following articles:

### Provisioning SSL Certificates

You can provision an SSL certificates using our DNS API integrations by following either of these guides:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

