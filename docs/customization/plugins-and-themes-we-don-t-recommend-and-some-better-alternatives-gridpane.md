# Plugins and themes we DON’T recommend (and some better alternatives) | GridPane

# Plugins and themes we DON’T recommend (and some better alternatives)

 

4 min read 

## Introduction

We don’t ban any plugins on your GridPane servers, and we never will. You are absolutely free to use the plugins you want. There are, however, some plugins that we dislike, and some that simply don’t work very well with GridPane.

These are general guidelines based on information available at the time of writing. We’ll update this article over time as more information becomes available.

 

## Plugins to Avoid

### Broken Link Checker

Notorious for causing performance issues. There are free, non-Wordpress alternatives that won’t eat up your servers resources. Check out ahrefs free tool instead.

### WP Bakery

Sure, it’s definitely improved over time, but there are literally services dedicated to cleaning up after it. I just don’t see a use case where this plugin makes sense. Why use it when Elementor and Beaver Builder exist? Also, with WordPress 5.5 even Gutenberg is looking pretty awesome now it’s starting to mature.

### Revolution Slider

You can definitely build cool sliders with it. It’s just bloated, slow, and has had severe security flaws in the past – reportedly resulting in 100,000+ hacked sites. I’m afraid no replacement recommendation for this one as close alternatives suffer some of the same problems.

Sliders typically aren’t great for conversions and none of our team has used a slider in some time.

### Contact Form 7

The team has mixed feelings about it. I always liked it, but we’ve seen a few issues with it recently (although the developer did fix them pretty quickly) and it loads on every page, regardless of whether it’s being used.

### Enable Gzip Compression

Gzip is already enabled by default on GridPane.

### WP phpMyAdmin

This plugin isn’t a great idea to begin with, but you can access phpMyAdmin for all your websites in your GridPane dashboard.

### SweetCAPTCHA

The WordPress Plugin Repo banned this plugin after it was used to distribute malware. We’re including it here simply for that reason.

### Disable XML-RPC-API

We have a security measure that does the same thing at the server level, rendering this plugin completely unnecessary. It also incorrectly writes to .htaccess on OpenLiteSpeed servers causing syntax errors. Uninstall on any sites you have it active.

 

## Caching Plugin Guidelines

If you’re using our server caching, then to prevent any conflicts don’t use any plugins other than Nginx Helper and GridPane Redis Object Cache.

If you’re not using our server caching, then you may want to check these out, in order: –

Start with Swift Performance and work your way down. Swift is likely the best non-server caching plugin available. The rest are pretty solid. Obviously don’t use Litespeed Cache on Nginx servers.

 

## Good Plugins, Just Not for GridPane

### Duplicator

Duplicator is an excellent plugin, we have no hard feelings against it at all. It just doesn’t work well with GridPane with the wp-config.php file being located outside of htdocs.

Instead, we highly recommend All in One WP Migration for migrations and backups, and also Migrate Guru for migrations.

 

## Don’t Use Nulled Plugins

This is just a bad idea all around. It’s theft and it’s inherently insecure. Nulled plugins may be modified wreck your site, open up vulnerabilities, or steal information. Please don’t used nulled plugins on any of your websites.

 

## Beware of Themeforest

This is just a general guideline.

There are undoubtedly some well made, high-quality themes on Themeforest. The Squaretype theme, for example, looks great and is used by 2 people I know of who are very knowledgeable – one a very knowledgeable GridPane user and the other a WP performance specialist.

However, a huge amount are ultra bloated, poorly constructed, and poorly maintained. Many are also insecure as the plugins they’re bundled with often have no way to update to the latest version. This is asking for trouble.

Getting a refund for a crap, unsupported, unusable and/or outdated theme is next to impossible. If the theme you buy isn’t a great seller then I wouldn’t expect updates or timely support.

A good rule of thumb is to check whether the theme demo is the up-to-date version of that theme. If it isn’t, then approach with caution.

If you’re confident that a specific Themeforest theme is solid, then great. If you’re unsure, save yourself the hassle, and go with a reputable, well supported theme with a good user base and history of good support and good reviews.

 

## Themes We Like

There are many great themes, but here are some that our team have used, like, and have good reputations:

Genesis is a paid theme. Oxygen is a paid plugin (visual site builder) that will deactivate any theme you have installed. Kadence, Blocksy, Suki, Astra and GeneratePress have free and paid options.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

