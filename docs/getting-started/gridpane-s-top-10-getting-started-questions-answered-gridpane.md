# GridPane’s Top 10 Getting Started Questions Answered | GridPane

# GridPane’s Top 10 Getting Started Questions Answered

 

6 min read 

## Introduction

When new users are getting started on the platform, there are a handful of questions that come up over and over. This article is designed to give you quick answers to our top 10.

### Table of Contents

If you’re getting started on a Core account, you may also want to check out this article as well: Core Plan: New Account Q&A

 

## 1. Getting Started: Choosing your first server provider

If in doubt, we recommend you get started with Vultr High Frequency.

Once you’ve added your API key you’ll see the high-frequency options in the dropdown priced at $6 intervals (6, 12, 24, 48, 96, etc). We also recommend that you check the box to enable server backups directly at Vultr. These do cost extra, but they are excellent insurance and well worth it. You can also get $100 free credit to get started.

 

## 2. Getting Started: Creating your first website/s

When creating new websites you’re presented with numerous options. If in doubt, you can simply stick with the defaults and you’ll be absolutely fine, and you can always make changes once the website is built.

The one thing you should absolutely do for every single website is to create its own unique system user. This will isolate all of your websites from one another at the server level, meaning that what happens on one website cannot affect all the others. This is an important security measure that, should the worst happen and one of your sites is compromised, means it cannot cross-contaminate all of the other websites on your server.

 

## 3. Migrations: The two best plugins we recommend

The two plugins that we recommend the most are All in One WP Migration (AIOM) (especially when migrating from Flywheel) and Migrate Guru. Both of these are excellent and the vast majority of the websites that have been migrated to GridPane have been done so with these two plugins.

Migrate Guru is 100% free and it’s generally very, very reliable. AIOM is free for websites below 512MB in size and is very easy to use. You can extend that a bit further if you export the files and database separately. Here are our knowledge base articles:

 

## 4. Migrations: The wp-config.php file is in the wrong place

To keep your WordPress configuration file (wp-config.php) secure, at GridPane it’s stored one level above your websites /htdocs folder. Your wp-config.php file contains your database username and password along with other information about your website, and so we keep it hidden and protected.

A common issue that we see when clients are migrating their websites over to GridPane is that they have an extra wp-config.php in the /htdocs directory, which can result in the website not displaying correctly. The fix is to simply rename or delete this file, and then you’re all set.

 

## 5. Migrations: Incorrect database table prefix

If you have imported your site, but all the plugins are deactivated and content is missing, then it likely means that your database table prefix needs changing inside your wp-config.php file. This section of our diagnosing migration issues knowledge base article demonstrates how to quickly fix this:Fix: Incorrect Database Table Prefix

 

## 6. Getting Started with DNS Records

Many new GridPane clients have never had to manage DNS records before. DNS stands for Domain Name System. In a nutshell, it’s used to point a website domain towards the IP address of the server where it’s hosted. There are many different types of DNS records, but to use your website/s with GridPane, you will need to be familiar with two: The A Record and CNAME Record. If you’re new to DNS, this article offers a simple 4 minute tutorial with a video:Setting DNS Records

 

## 7. SSL Certificate Failed to Provision: DNS records aren’t pointing to the server

The most common SSL issue that we see is that the DNS records are not yet pointing to the server before turning SSL to ON. To prevent abuse, Let’s Encrypt needs to first verify your domain, which requires live A and CNAME records for your URL. You can easily check this with a website like:https://dnschecker.org/#A

And to speed things up, you can use a high-quality DNS provider like Cloudflare, which is also 100% free.

 

## 8. Caching: Our Recommendations

If in doubt, use Redis Page Caching AND Redis object caching on Nginx servers, andon OpenLiteSpeed the choice is easy, use both LS caching and Redis object caching. You can learn more about our server-level caching options here:An Introduction to GridPane Server Caching Options

 

## 9. Caching: Common issues with pagebuilders

A common issue we see reported with pagebuilders like Elementor, Divi, Beaver Builder, etc, is that sometimes the pages on a site look a little like broken HTML.

This is due to the way these builders use and update stylesheets. The simple fix is to clear the cache for the page once you make an edit to that page, which will then load the latest version of that page’s stylesheet into the cache. Also, after updating pagebuilders plugins you may also find that the updates rewrite stylesheets as well, so you may also want to check and clear the whole site cache after these updates.

Further, comprehensive info on troubleshooting website caching can be found here:Diagnosing Caching Issues

 

## 10. SMTP: Emails aren’t being delivered

Unlike most shared hosting, when you move to the cloud you will find that you don’t have an email solution automatically provided. Actually, we strongly advise against setting up an email server on any server hosting websites, and GridPane does not configure an email server on any GridPane managed box.

Email delivery is serious business, and it’s important that it be treated seriously, and not as an afterthought. This means you’ll need an SMTP solution. We have a simple integration with SendGrid that can make this task straightforward, or you could also use a plugin like FluentSMTP which you can use to connect to all the major providers like Postmark, Amazon SES, Mailgun, etc.

The most common reason we see emails not being delivered is that the SMTP provider requires you to authenticate the domain with their service. After that, it’s smooth sailing.

For our SendGrid integration, here’s how to troubleshoot any issues you may run into:Troubleshooting the SendGrid SMTP Integration

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

