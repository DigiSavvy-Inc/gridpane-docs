# Getting Started with Relay and Object Cache Pro | GridPane

# Getting Started with Relay and Object Cache Pro

 

4 min read 

### Table of Contents

 

 

### Relay and the Ubuntu 20.04 OpenLiteSpeed Stack

Due to missing dependencies (non-existent lsphp packages for Relay) our Ubuntu 20.04 OpenLiteSpeed (OLS) stack does not support Relay and OCP. This may be possible in the future, but no current ETA.

Relay and OCP are supported and available on the newer 22.04 OLS stack.

## Introduction

Relay is a new powerhouse in the WordPress performance world that allows you to cache your database for ultra-fast dynamic page loading, with the additional benefit of saving server resources with Relay Redis and Object Cache Pro.

### Relay

Relay keeps a super-efficient partial replica of Redis data in PHP’s memory, offering a massive boost to WordPress speed. It effortlessly manages millions of requests per second, minimizing Redis communication and saving server resources and bandwidth.

### Object Cache Pro (OCP)

Object Cache Pro is the upgrade to the free Redis object cache plugin. When combined with Relay, this is extremely powerful for WooCommerce, LMS sites, BuddyBoss, or any dynamic sites where users are actively logged in/managing the backend.

 

## Relay and OCP Licensing

Licensing for Relay and the Object Cache Pro plugin covers usage for 1 website URL and all staging sites across multiple servers.

For example, if your domain is mybusiness.com, your license also covers staging.mybusiness.com, and this site can live on multiple servers and still use the same license on each server.

If you also wanted to use it on a subdomain, for example, shop.mybusiness.com, this would require its own license.

### License Tracking

Your licenses are tracked within your account (more details below).

 

## Activate Relay and OCP on Your Websites

You can activate/deactivate Relay and Object Cache Pro for your websites via your account dashboard (recommended) and via GP-CLI.

To activate within your GridPane dashboard, head over to your Sites page and click on the name of the website to open up the website customizer. From here, open up the Caching tab and click through to Object Caching:

You can use to toggle to activate Relay and OCP, and later deactivate if you ever need to do so.

Licensing is automatically tracked within your account, and here you can also see the number of unused licenses available.

Please note that activation can sometimes take 1-2 minutes, so please be patient while the installation process takes place..

 

### Installation via GP-CLI

This currently needs to be done by connecting to your server via SSH and using GP-CLI. If this is the first time connecting to your server, please see the following guides:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Enable Command

Connect to your server and run the following command (replacing {site.url}, {ocp.license}, and {relay.license} with the appropriate information):

```
gp site {site.url} -enable-object-cache {ocp.license} -relay {relay.license}
```

For example:

```
gp site yourwebsite.com -enable-object-cache 5Ke3SM5yAcxlAlL4XeoTbswH9 -relay nd3ohEc6JuXocyNkcevOnzgXp
```

### Disable Command

```
gp site {site.com} -disable-object-cache {ocp.license} -relay {relay.license}
```

For example:

```
gp site yourwebsite.com -disable-object-cache 5Ke3SM5yAcxlAlL4XeoTbswH9 -relay nd3ohEc6JuXocyNkcevOnzgXp
```

 

## Installation Information

### Object Cache Pro is a Must-use Plugin

Once activated (as above), the Object Cache Pro plugin is installed as a must-use plugin, so it won’t appear in the normal plugin list. You’ll need to click through to the must-use list if you wish to confirm it’s installed:

### Plugin Settings

The Object Cache Pro settings and status can be found in the WordPress admin dashboard under Settings > Object Cache:

 

## Staging, Cloning, and Cloneover

Right now, we have a guard in place that will run a check at the beginning of the staging or cloning process, and if Object Cache Pro is detected at either the source site or destination site. If detected, we will send a notification to your dashboard stating that you might need to take further action via GP-CLI for the destination website in order to continue using Relay and OCP or deactivate it.

Below is a quick breakdown.

 

### Staging and Cloning/Cloneover to the Same URL

 

### Cloning/Cloneover to a New URL

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

