# Creating a Blueprint (AKA Boilerplate) WordPress Website to Speed Up Development | GridPane

# Creating a Blueprint (AKA Boilerplate) WordPress Website to Speed Up Development

 

3 min read 

### Table of Contents

 

## Introduction

GridPane has a handy Bundles feature that allows you to pre-install your preferred theme and plugins on your sites when you create new websites, but many of our clients (and myself included back when I designed offered web design services) will take an even more efficient approach.

This is what we call a Blueprint website (AKA a Boilerplate site), which is a partially built-out site that you simply clone to your development domain, and that cuts out all the foundational groundwork that you may normally do for each and every project.

This isn’t a feature in itself, but GridPane makes utilizing a Blueprint site in your business extremely easy. In this article we’ll take a look at some use cases for Blueprint sites, and how to use them effectively on GridPane.

 

## Building Your Blueprint Website

The purpose of the Blueprint site is to save you time. As an example, my own version of this had the following:

There’s probably a handful of other settings as well, and the sky’s the limit.

### Building it out

I used the beginning of a real project to build out my Blueprint. I was doing the work anyway, and I took that opportunity to create it then. How and when you do it doesn’t really matter though, and you can also build out more than one.

For example, we have clients who have an Elementor Blueprint, an Oxygen Blueprint, and a WooCommerce Blueprint. Depending on the project, they simply choose the right starter template for it.

 

## GridPane Workflow

Below are a few recommendations for developing on GridPane.

### 1. Activate GridPane Security Features

When developing a new site it’s a good idea to do so with all the security features active. That way, should any kind of false-positive occur, you can identify it and fix it before setting the site live.

You can learn more about the security features we have available for your websites in this article:

Secure Your WordPress Websites: An Overview of the Security Tab

This would include your WAF of choice (probably 7G in most cases), Fail2Ban, and all or most of the additional security settings.

### 2. Leave Caching Turned Completely Off

There’s no benefit to turning caching on for a site that’s in active development. It may actually confuse things for yourself or the client when checking your work. Caching can easily be activated once the site is set live, but is better left OFF until then – that applies to both page and object caching.

### 3. Cloning

My Blueprint website address used to be blueprint.mydomain.com. You may want to do the same.

When taking on a new client, the GridPane cloning feature makes it extremely easy to clone the site to clientname.mydomain.com and then begin your work.

Also, when you clone your Blueprint to the site you’ll be developing on, all of the security tab settings will be cloned over, so you don’t need to activate them all a second time. The same goes for any kind of Nginx or OLS configuration file you’ve created on the server, any PHP settings you may have adjusted (usually not necessary as our defaults are ideal for most sites), and the user-configs.php file.

Before you clone you can also force update the site.

### 4. Set it Live

When you’re ready to set the site live, simply use our cloning feature again to clone the dev site to the clients domain.

Turn on caching, provision an SSL, and you’re good to go!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

