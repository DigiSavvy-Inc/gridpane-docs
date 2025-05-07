# GridPane News and Last Month in Review (Oct 2021) | GridPane

# GridPane News and Last Month in Review (Oct 2021)

 

6 min read 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1023'%20height='683'%20viewBox='0%200%201023%20683'%3E%3C/svg%3E)

## Intro

October was an important month for GridPane. We officially released our Preemptive Support “360” service, and this is now publicly available.

We also had a busy month on the development side, and we published several new knowledge base articles. Below we’ll take a quick look at the:

 

## 360 Preemptive Support Launch

This release marks an important milestone in GridPane history: Our Preemptive Support “360” service is now publicly available.

360 is OUR version of what we believe true managed WordPress should actually look like. It’s a much more comprehensive approach to anything else out there that we’re aware of, and it means that our team can now offer site-specific support in a holistic, sustainable way.

If your websites go down in the middle of the night, we’ll know about it and begin working to resolve it, so you can sleep easy knowing that we have your most important websites covered.

More than that though, 360 allows our team to see your site and server problems BEFORE they become critical.

Our systems will monitor your websites, servers, and notifications, and should we identify any issues, these will automatically create a support ticket for our team.

As we always do here at GridPane, there is a special bonus offering for fast movers. All the details can be found here:

https://gridpane.com/360-support/

 

## Changelog

The changelog is up-to-date for the whole of October (a lot has also been pushed today and this will be added later this week). Notable updates include final fixes for beta features:

This has all been in preparation for their full release out of beta and into production – which is today!! Backups V2 and OpenLiteSpeed are now officially out of beta 🙂

via GIPHY

UpdateSafely™ had a few updates as well, but it’s still in beta for now. If you have the opportunity to test it on a non-production server, please do. All feedback is valuable to move beta features forward.

You can view the full changelog here:https://roadmap.gridpane.com/f/changelog/

 

## Knowledge Base Additions

We published numerous articles in October, and there are a few notable inclusions that may be of interest to many of you.

### 1. Diagnose and Fix Common Issues Learning Path

Just underneath the search bar on the Knowledge Base page, you have hopefully already seen our 3 learning paths listed out. The Diagnose and Fix Common Issues page has been given a full overhaul to include all of our additional troubleshooting documentation and a layout update breaks things down into categories.

The solution to almost every issue you may encounter on GridPane is contained within these articles – and most of this information isn’t GridPane specific and so transfers to hosting in general.

Please be sure to check it out and consider bookmarking it for future reference. If you want to become a pro at using the GridPane platform, these articles will teach to you all the most important fundamentals.

https://gridpane.com/knowledgebase/problem-solving/

### 2. Install and Configure New Relic on GridPane Servers

This is an article that has been on my to-do list for some time, but thanks to Sean Vandermolen from the community for dropping a ton of useful information in the GridPane Facebook group I was able to move it forward.

The article contains instructions for both Nginx and OpenLiteSpeed servers, and a few other notes that may be helpful. You can check the article out here:

Installing and Configuring New Relic for WordPress

### 3. Provision a Katapult Server

Katapult is a relatively new IaaS provider that we are pretty damn impressed with. We’re hosting our StudyEthic LMS that contains all our training courses on Katapult, and use it for various other projects as well.

They offer a generous amount of free credits to get started and they are powered entirely be legitimate green energy. This article will walk you through how to add a Katapult server using our custom server option (it’s quick and easy):

Provision a Katapult Server using our Custom Server Option

### 4. Autopurge the Cache After Updating Core/Theme/Plugins

This particularly useful code was put together by a GridPane client, and instructs the Nginx Helper plugin to purge the cache when:

This can be particularly useful for websites that use pagebuilders due to the way they implement CSS. Check it out here:

Automatically Purge the Cache on Updates via Nginx Helper Hooks

### Additional Articles We Published in October

Other newly published articles include:

 

## November 1st News

It’s too big a day to not mention the things that have been released today along with this post. We’ll cover them next month too, but here’s a rundown:

We’ve dropped some major updates today and here’s a quick rundown of what’s been pushed.

### Backups V2

Backups V2 is out of Beta. It’s been a long road to get here, but it is officially ready to go for everyone on the platform.

All new server builds will now run on the new V2 backups. Your pre-existing V1 servers have NOT been updated and they will continue to run, but you can upgrade via the backups tab in the server customizer at any time. You will never be forced to upgrade, but we’re potentially looking at the end-of-life for V1 being early December – more details will follow on that nearer the time.

### OpenLiteSpeed (OLS)

OLS is out of beta. Final bug fixes have been ironed out and all updates have been pushed out today. A tremendous amount of work has gone into our OLS stack and we’re excited to finally release it into full production.

### PHP 8

PHP 8 is available for Nginx/PHP-FPM stack, and we’ve also updated system defaults and app build defaults to PHP7.4. LSPHP8 is not available for OLS yet – they have yet to compile the lsphp80-Redis package we need for symmetry with the Nginx stack and UI, but we are looking at compiling this ourselves in the short term. Note that WordPress generally isn’t ready for PHP 8, so if you experience weird behavior on a site, make sure you thoroughly check it over with PHP 7.4 as you may find this fixes the issue.

### 7G WAF

The 7G WAF will be updated to v1.4, but it has been postponed a day or two, while we update Jeff Starr with some issues we discovered with the vanilla Nginx rules. We do intend to keep parity with the official ruleset but will roll out our version in the short term.

 

## And that’s a Wrap

Until next time!Steve

 

 

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

 

 