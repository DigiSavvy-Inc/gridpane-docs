# Speeding Up DNS Propagation: Manually Clearing Out Cached Records | GridPane

# Speeding Up DNS Propagation: Manually Clearing Out Cached Records

 

1 min read 

### Table of Contents

 

## Introduction

Nowadays, DNS is pretty quick to “go live” worldwide, usually taking minutes instead of the older “24-48” hours standard.

Even GoDaddy, in my (thankfully) limited experience working with them over the last few years, propagates new records within 5-10 minutes – usually the former.

That said, we do see tickets in support where things are taking considerably longer than normal to go through. This article will offer a few tips to speed things up when needed.

 

## Understanding DNS Propagation

“DNS Propagation” is the time it takes to publish or update DNS records. This is usually instantaneous at most providers and, at most, may take a few minutes at lesser quality providers.

What actually takes time and causes the “24-48” hour delays you often see notices about is the clearing of the previously cached version of these records across the internet.

A great article by Julia Evans that digs much deeper into this and is well worth a read to learn more is:

DNS “propagation” is actually caches expiring – by Julia Evans

Below, we’ll look at how you can speed this process up.

 

## Manually Clearing Cached DNS Records

The following three websites will help you clear out previously cached DNS records to speed up the worldwide. Simply visit each site and run the cache clear:

You’ll want to make sure you flush both the primary record and the www record.

You can then check your DNS records worldwide at:

https://dnschecker.org/#A(If you haven’t already, we recommend bookmarking this website).

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

