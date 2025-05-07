# GridPane News and Last Month in Review (November 2022) | GridPane

# GridPane News and Last Month in Review (November 2022)

 

6 min read 

 

## Introduction

Hey WordPress Warriors! November saw Black Friday and Cyber Monday come ago, the release of Developer PLUS, and numerous feature and knowledge base updates. We’ll dig into everything below.

### Table of Contents

 

## Black Friday – Cyber Monday

The big event in November was, of course, our Black Friday presale, followed by the public Black Friday – Cyber Monday sale for Developer Plus. Feedback on the deal was overwhelmingly positive, and thank you so much to everyone who jumped on board.

 

## Price Increases and Developer PLUS

Our prices for the Panel plan were also raised on Black Friday, and Developer features are now only available if purchased with the upcoming third-party services as a part of Developer PLUS.

Please note that if you created your account before Black Friday, your existing pricing will remain exactly the same, and the new prices only apply to new sign-ups.

### Developer PLUS

The additional third-party features that will soon be included with Developer PLUS are:

These will be available in 2023 Q1. Our Q&A video can be found over on our YouTube channel here, and you can view our Fortress Security plugin Q&A below:

 

 

## Changelog

You can check out all of the fixes and improvements on our roadmap here: https://roadmap.gridpane.com/f/changelog/

### UpCloud API Update

UpCloud updated their API  to include their new plans in early November. This update broke new server build functionality with our integration. This was quickly fixed after the issue was identified, and we also separated their plans out in the server dropdown to make it clear and simple to select the server you’re looking for.

### OpenLiteSpeed Vulnerability (Patch Implemented)

On November 10th, cybersecurity firm Unit 42 publicly disclosed three vulnerabilities that they discovered in OpenLiteSpeed (OLS).

This was a vulnerability from the OpenLiteSpeed itself, not GridPane. It also affected LiteSpeed Enterprise. All GridPane OpenLiteSpeed servers were quickly patched.

You can read Unit 42’s public disclosure here: Unit 42 Finds Three Vulnerabilities in OpenLiteSpeed Web Server

### Significant Servers Page Load Time Improvements

If you’re running a lot of servers, then the Servers page inside your GridPane account should now load significantly faster. Numerous things have been refactored behind the scenes so that the pages within your account dashboard still load fast, no matter how many sites or servers you host with us.

### Debug Added to the SendGrid Integration

To make troubleshooting easier, debug output from our integration is now sent to the WP_DEBUG log.

 

## PHP CLI Update

All versions of PHP are now available for CLI on all Nginx and OLS servers. The default has also now been updated from PHP 7.4 to PHP 8.0.

This update will NOT affect the PHP version of your sites. PHP CLI is PHP’s Command Line Interface, and it allows PHP to be executed from the server command line. Your website’s PHP version and the server CLI PHP version are independent of each other.

### Setting Nginx and OLS CLI PHP Brought to Parity

We also released an update to bring Nginx and OpenLiteSpeed into parity, so setting a custom version now works the same, no matter which stack you’re using. Further details on PHP CLI can be found in this knowledge base article:

Setting the CLI PHP Version

 

 

### IonCube Loaders Info

IonCube Loaders have skipped PHP 8.0, supporting only PHP 7.4 and PHP 8.1. If you have IonCube Loaders installed on your servers, you will need to manually adjust your PHP CLI version in order for them to work. Full details can be found in this knowledge base article:
How to Install Ioncube Loaders

## Newly Published Knowledge Base Articles

We published 2 new articles in November. The first details how to implement a custom server-wide user-configs.php as detailed in the new releases above, and the second is the solution if a site or tool is reporting your site as being insecure, when that’s not actually the case.

 

### 1. How to Create a Custom Server-Wide user-configs.php File

Instead of editing the wp-config.php file directly, GridPane uses an include called user-configs.php, where you can safely add your own wp-config.php edits.

In this article, we take a look at how you can create a server-level user-configs.php file that will automatically get applied to any new websites that get created on your server.

How to Create a Custom Server-Wide user-configs.php File

 

### 2. Why Do SEO Tools / LinkedIn Say My Website is Insecure?

At the time of writing, if you’re forcing TLS 1.3 on your websites, LinkedIn, as well as some SEO tools, will report that your website is insecure, even though you have an active SSL and are using the latest secure protocols.

This is due to them not supporting the latest TLS version (despite the fact that TLS 1.3 was released in August 2018) and is a quick and easy fix.

Why Do SEO Tools / LinkedIn Say My Website is Insecure?

 

## Knowledge Base Updates

In addition to the 2 new articles above, the bulk of the time spent on the knowledge base was spent tweaking and updating the following 26 articles:

 

## That’s a Wrap!

Thanks for reading. We’ll continue to keep you posted in the weekly newsletter. Have a great December everyone!

 

 

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

 

 