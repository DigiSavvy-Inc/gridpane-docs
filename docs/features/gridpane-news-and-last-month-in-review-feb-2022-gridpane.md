# GridPane News and Last Month in Review (Feb 2022) | GridPane

# GridPane News and Last Month in Review (Feb 2022)

 

6 min read 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='673'%20viewBox='0%200%201024%20673'%3E%3C/svg%3E)

## Introduction

Hey WordPress Warriors! February is on the books, and here’s a rundown of some of the behind-the-scenes work that went on. This includes new releases, 7 new knowledge base articles, 28 knowledge base updates, and an update on the status of backups V1.

### Table of Contents

 

## New Releases

### GridPane Nginoil

Nginoil is an optional feature that runs as a part of the nginx.service when it starts up. Unlike a regular start-up that runs a standard nginx -t, Nginoil has built-in functionality to detect where Nginx syntax errors are originating from and implement a fix that allows Nginx to successfully boot up. It can be activated via GP-CLI, or there’s also a toggle in the Server Customizer > Nginx tab, so you can easily activate/deactivate this directly inside your GridPane dashboard.

GridPane Nginoil – Automatically Fix Nginx Syntax Errors

Along with Nginoil came some updates to our gp nginx -t and gp nginx reload commands. Details are also in the above article.

### GridPane API

Support for PHP 8.0 in OAuth API was also introduced.

 

## PeakFreq

We’re launching our internal pilot program for PeakFreq, which is our take on “managed WordPress meets the fastest infrastructure on the planet.” Over the past 18 months, we’ve tested everything under the sun as relates to “high frequency” and we’ve landed on a handful of configurations that we feel sufficiently move the needle in performance – particularly for any kind of high concurrency WooCommerce and LMS type workloads.

The hyper short version: you need to have production-ready Woo/LMS/complex workloads that need rocket fuel, and you want us to handle everything. You can learn more about this here in the Facebook group.

We’ll also publish additional information on this to the blog in the near future.

 

## Changelog

The changelog has been updated and can be viewed over on our roadmap here:

https://roadmap.gridpane.com/f/changelog/

### Notable Fixes/Improvements/Changes

 

## Newly Published Knowledge Base Articles

We published 7 new knowledge base articles in February. Some of these may be of particular interest to many of you.

### OpenLiteSpeed (OLS) Caching and the LiteSpeed Cache Plugin (LSCache)

We published our long-awaited article on activating page and object caching on OpenLiteSpeed and using the LiteSpeed Cache plugin. Links to the official documentation for further information have been added throughout the article alongside our breakdown.

This article is intended as a getting started guide rather than an in-depth look at every one of the plugin’s extensive list of features.

OpenLiteSpeed Caching and the LiteSpeed Cache Plugin

### How to Reduce Eric Jones Spam (and all the other Contact Form Spam)

Recently, one of my sites started getting relentlessly hammered with “Hey, my name’s Eric and for just a second, imagine this…“, as well as a bunch of other junk that landed straight in my spam folder. It’s a nuisance, and spam is always a constant battle, so I figured I’d set out to solve this (at least until these spammers implement a workaround).

How to Reduce Eric Jones Spam (and all the other Contact Form Spam)

### Creating a Blueprint (AKA Boilerplate) WordPress Website to Speed Up Development

Going a step beyond our bundle’s feature, many WordPress professionals use what’s known as a Blueprint website (AKA a Boilerplate site). This is a partially built-out site that you simply clone to your development domain, and that cuts out all the foundational groundwork that you may normally do for each and every project.

This isn’t a feature in itself, but GridPane makes utilizing a Blueprint site in your business extremely easy.

Creating a Blueprint (AKA Boilerplate) WordPress Website to Speed Up Development

### Additional Articles

We also published the following:

 

## Knowledge Base Updates

In addition to the 7 new articles above, in February we updated 28 existing articles:

 

## Backups Update

Backups V1 has now been removed from the UI now that we’re 3 months on from their official end of life, and 4 months on from the V2’s release out of beta. They can still be managed directly via CLI on the server (details in the knowledge base), but we highly recommend updating to the new V2 system as soon as possible.

A script that was planned for removing V2 backups older than February 25th, 2021 that were a part of the early beta was slightly delayed – we’ll update the status on that here ASAP. More details on this can be found in this blog post:

Backups Announcements: V2 Pre Feb 25th 2021 Backups, and Goodbye to V1

 

 

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

 

 