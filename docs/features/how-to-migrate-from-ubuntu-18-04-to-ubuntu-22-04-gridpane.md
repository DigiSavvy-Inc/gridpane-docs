# How to Migrate from Ubuntu 18.04 to Ubuntu 22.04 | GridPane

# How to Migrate from Ubuntu 18.04 to Ubuntu 22.04

 

5 min read 

 

### Ubuntu 18.04 Servers are no longer supported

GridPane stopped support for servers with Ubuntu 18.04 on May 1st, 2024.
Our support team is no longer able to handle support tickets generated from these servers, or sites on these servers. Please be sure to move your sites to a 20.04 or 22.04 server as soon as possible.

 

### PHP 7.3 & 7.4 Notice

If you still host websites that are incompatible with PHP 8+ and are unable to update them, PHP 7.3 and 7.4 are available on our Ubuntu 20.04 stack. Ubuntu 22.04 only supports PHP 8.0 and above.

### Table of Contents

 

## Introduction

For those of you beginning to migrate from Ubuntu 18.04 servers, our cloning scripts are fully compatible with both the 22.04 and 20.04 stacks. However, as with any migration, please ensure you thoroughly test that all your sites have migrated successfully before deleting your original servers.

 

 

### Information

Our Ubuntu 22.04 stack comes with some significant upgrades. If you haven't already, we recommend that you read this article:
The Ubuntu 22.04 Stack Feature Updates

## How to Upgrade

The easiest way to move your websites is to create a brand new server and then use our full server clone functionality to clone all of your websites in one go. Details on this feature can be found here:

Cloning One Entire Server to Another

Important: Unfortunately, it’s not possible to support upgrading a server’s OS. This is not the straightforward process that it appears to be on the surface, and it can’t simply be automated. Each stack is built specifically to be compatible with each version of the Ubuntu OS and the different software/packages/modules that support it. This means you need a new 22.04 server.

 

## Vultr: Keep Your Existing Server IPs and Avoid DNS Changes

Vultr allows you to convert your existing server IP addresses into “reserved” IP addresses (commonly known as floating IPs). This can potentially save you a great deal of time, and Vultr outlines the process in the following article – but please ensure you follow the guidance immediately below before deleting existing servers:

Vultr: Convert an Existing IP to Reserved

 

## IMPORTANT: Check Your Websites Before Deleting Your 18.04 Server

Our cloning tool is extremely reliable and will work without issue for almost all websites. However, no matter how reliable, you must always check your websites to confirm that they have been cloned successfully. You can do this via a local host redirect as detailed here before changing DNS / moving your floating IP address:

How can I edit my local hosts file to redirect URLs

 

## PeakFreq Managed Servers

Our PeakFreq-managed servers are also an option we’ve received a lot of inquiries about. This is also now available to everyone by making a deposit, and all PeakFreq servers run Ubuntu 22.04. You can learn more about PeakFreq here:

 

## Additional Resources

If you don’t already have a DNS management strategy in place for your hosting clients, now is an excellent time to implement one.

### Q&A

 

Can I clone sites from 18.04/20.04 servers to 22.04?

Yes, assuming your servers are all properly sized, and your website databases don’t have any serious issues.

If you’re running a full server-to-server clone, you will also be able to use remote backups from alternative sources for any that don’t play nice for any reason.

Easily Deploy a GridPane WordPress Site

And these articles will help you get started customizing your settings for even quicker deployments:

New WordPress Website Build Configuration Settings

Using Default WordPress Admin Settings to deploy GridPane sites

New Website Checklists

Why can’t you support new Ubuntu releases as soon as they come out?

There are numerous reasons why support for new OS versions takes some time. For example, we were waiting for specific Nginx updates before we released the 20.04 stack, and then ultimately ended up building those ourselves.

Here’s a rundown of the different factors:

Future stacks will continue to build upon the previous ones, and these may not always have such huge changes like the new system user functionality and directory structures, but we will always be at the mercy of the 3rd party packages we use, which can take 6-9 months or more to come out after the LTS release date.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

