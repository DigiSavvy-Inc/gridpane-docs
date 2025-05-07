# GridPane News and Last Month in Review (July 2022) | GridPane

# GridPane News and Last Month in Review (July 2022)

 

6 min read 

 

## Introduction

Hey WordPress Warriors! July saw lots of behind-the-scenes work take place for the new Git integration and a major update to our multitenancy feature. We’ll cover these and the regular knowledge updates below.

### Table of Contents

 

## The GridPane Git Integration

The Git integration has received a wide range of updates and upgrades. The bulk of these were released towards the tail-end of the month and are all documented on our changelog.

The main ones include further integration into our existing features, including major upgrades with regards to the following features:

Quick note: The Git integration is still currently in private beta.

### Staging and Cloneover

The staging and cloning features all now work seamlessly whether the source, destination, or both sites are configured for Git. This includes both Full and Hybrid Git integrations, and the new Multitenancy Git server update.

One important note here is that when the destination site is configured for Git, Git-managed files will not be affected and you should ensure that these sites have the necessary themes and plugins to work correctly configured as a part of your repo when making a staging push or cloning over an existing site.

You have a choice of pushing both the database and the uploads directory, or only the database, or only the uploads directory.

### Cloning

Git configured sites can be cloned just like normal websites.

When cloning into a multitenancy server, the codebase of the destination site will already be configured via Git, so again like cloneover and staging, it’s important that your repo has the necessary components for the clone to be successful.

### Backups V2

Our V2 Backups system has received multiple updates to make restoring backups to Git websites.

Additional good news here is that these additional features extend to your regular non-Git configured websites as well (more on this below)

When restoring backups you have the ability to:

For Git configured websites, this means the codebase is always in alignment with the Git repository it’s attached to.

 

## GridPane WordPress Multitenancy

In conjunction with the new Git features, our multitenancy solution has been updated to take advantage of the same scripts and feature integrations. You’ll find that there is a lot of cross-over between how the two work inside the UI.

Multitenancy now also uses the same Full Git Repository as standard Gridane Full Git Integration.

This is a major update that makes the feature set a lot more accessible in terms of usability and making the most out of the entire of GridPane tools.

The “immutable blueprints” section inside of the settings page has also been removed and replaced with a new tab inside the server customizer called “Multitenancy Git” which makes the management of these servers easier than our previous iteration.

Multitenancy is available on Agency Plan.

 

## V2 Backups Restores

This significant update was introduced so quietly by our dev team that I almost missed it entirely. Along with the Git updates for backups, you now have the ability to run the following restores on your regular WordPress websites:

This allows for more granular restores, and will also potentially save time on websites that are large in size.

Updates to backup imports are also in the works and are set to go live this week.

 

## PanelPress.io: Client Portal Update

The Client Portal is currently built on a platform called Bubble. This has allowed us to build a solid first iteration, however, the limitations of this platform mean that it’s not viable for the long haul and our future plans.

Currently, this undergoing a complete rebuild, and this will be the next major update.

 

## Changelog

The changelog has been updated. The major releases are detailed above, and you can check out the other fixes and improvements on our roadmap here:

https://roadmap.gridpane.com/f/changelog/

The main updates/releases in July were the Git integration and bringing our Multitenancy solution in line with the new Git feature set.

 

## Newly Published Knowledge Base Articles

We published 5 new articles in July:

### 1. Using GridPane Multitenancy

In this article, we’ll walk you through the process of setting up your multitenancy servers and take a look at the primary use cases and how it compares to WordPress multisite.

Using GridPane Multitenancy

 

### 2. V2 Backups Part 4. Troubleshooting & Backups Failure Notifications

Prior to this article, we had another article dedicated to troubleshooting Monit notifications for backup failures. The contents of that article has been updated and rolled into this article.

Two additional sections on troubleshooting are available in this update:

V2 Backups Part 4. Troubleshooting & Backups Failure Notifications

 

### 3. A Beginners Quick Start Guide to Git for WordPress

The goal of this article is to provide a simple quick start guide for anyone who is brand new to using Git and wants to begin learning. It covers the absolute basics necessary to get up and running, which means creating repositories and pushing them to GitHub.

This doesn’t cover any advanced topics, but there’s a section with links to additional resources for learning more, as well as the next steps in your GridPane-Git journey.

A Beginners Quick Start Guide to Git for WordPress

 

### 4. Getting Started with the Client Portal (PanelPress.io)

In this article, we take a quick walkthrough of the available options and where they live inside of PanelPress. For the most part, the Client Portal is intuitive to use, but a general overview can be helpful when first getting started.

Getting Started with the Client Portal (PanelPress.io)

 

### 5. How to Clear Your Website Caches (All Methods)

Technically this was published on August 1st, but the article itself was written in July. This wasn’t originally an article that had occurred to me to write, however, there was a request on our roadmap for an article dedicated to all the different methods available to run cache clears and also some general guidelines on when to do so.

How to Clear Your Website Caches (All Methods)

 

## Knowledge Base Updates

In addition to the 5 new articles above, the following knowledge base articles were also updated during July:

The Diagnose and Fix Common Issues page has also been updated to include the recently published backups troubleshooting article.

 

## That’s a Wrap!

Thanks for reading. We’ll continue to keep you posted in the weekly newsletter. Have a great August everyone!

 

 

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

 

 