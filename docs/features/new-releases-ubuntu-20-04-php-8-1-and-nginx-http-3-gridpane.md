# New Releases! Ubuntu 20.04, PHP 8.1, and Nginx HTTP/3 | GridPane

# New Releases! Ubuntu 20.04, PHP 8.1, and Nginx HTTP/3

 

3 min read 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1023'%20height='683'%20viewBox='0%200%201023%20683'%3E%3C/svg%3E)

We’ve just dropped some major updates and new releases to the platform. Here’s the rundown!

 

## Ubuntu 20.04

The much anticipated Ubuntu 20.04 release is now here, and it’s available for both Nginx and OpenLiteSpeed. This release has been a herculean effort from our team, and it comes with 3 different options:

More on the two different Nginx options now available below.

### Ubuntu 18.04

We’re of course still supporting Ubuntu 18.04 builds, and these are still available. As a whole, the 18.04 stack remains unchanged.

We will look to update Nginx to v18 shortly too, but there is an issue with proxy cache purging throwing errors above this version with the purge module, so v18 is likely the ceiling for this stack.

### 20.04 Nginx and FastCGI + ModSecurity

As mentioned above, beyond Nginx v18 the proxy cache throws errors when trying to purge with both FastCGI and ModSecurity active. On 20.04 these two features can no longer be used together.

### Migrating Sites to Ubuntu 20.04

Cloning from 18.04 to 20.04 is fully compatible, including cloning from Nginx to OpenLiteSpeed and vice versa, and you’ll find that PHP 7.2 and below have been removed, saving some memory on newly created servers.

Note that you’ll need to create a new 20.04 server and migrate your websites across. Due to the complex nature of upgrading an operating system with live production workloads, manually upgrading your Ubuntu version on existing 18.04 servers is not something we have the capacity to support (infact, such an upgrade would likely cost you several thousand dollars if hiring a sysadmin to perform this for you).

 

## Nginx HTTP/3 20.04 Beta Release

The hold up with 20.04 on our part has been that Nginx have planned to release support HTTP/3 going back quite sometime now, and we’ve been waiting on that release. Unfortunately, this still hasn’t come to pass and so we finally gave up waiting and we’ve instead built our beta from here:

This is available as an additional beta branch of Ubuntu 20.04 which you’ll see in the dropdown when you go to create a new server, and we would definitely encourage as much testing as possible if you have the time. As with anything in beta though, please don’t use it for important production websites.

 

## PHP 8.1 for Nginx, PHP 8.0 for OpenLiteSpeed

### Nginx

PHP 8.1 is now available for Nginx on new 20.04 servers. As noted above, PHP versions 7.3, 7.4, 8.0, and 8.1 are included.

Right now on the 18.04 stack is still at PHP 8.0 but we will look to bring 8.1 to this LEMP stack in the future.

### OpenLiteSpeed

We’ve also released PHP 8.0 for OLS on new 20.04 servers.

PHP 8.1 will come in the future, but like with PHP 8.0, the team behind LiteSpeed tends to take a long time to compile pecl extensions. We’ll release PHP 8.1 once support for it becomes available.

The 18.04 OLS stack PHP has no modules to upgrade to PHP 8.0 or 8.1 yet, and so this is only available on 20.04 servers.

### WordPress and Support for PHP 8.0/1

Please note that while you certainly can use PHP 8.0 and 8.1, a lot of the wider WordPress ecosystem (themes and plugins) is still not compatible yet and you may experience strange behavior within your site if that’s the case.

Switching back to 7.4 and retesting the functionality you’re experiencing issues with should always be a step in your troubleshooting.

 

## A New Lifetime Deal

Finally, remember how we said we might do another LTD in the future? Well today that has arrived, and you can learn more here:

Introducing the New GridPane Core Plan

 

 

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

 

 