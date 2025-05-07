# How Do I Reinstall GridPane Plugins? | GridPane

# How Do I Reinstall GridPane Plugins?

 

1 min read 

## Introduction

GridPane offers 2 server stacks that use different plugins to manage our server level caching. When you migrate a site in, these may be removed depending on the migration method.

### Nginx

When you spin up a new WordPress site on Nginx, we automatically install Nginx Helper, and the Redis Object Caching plugin.

### OpenLiteSpeed (OLS)

OpenLiteSpeed uses the LiteSpeed caching plugin to manage both page caching and Redis object caching, and we install this automatically on newly created OLS sites.

## Nginx Helper Plugin

To reinstall Nginx Helper, you can find this in the WordPress Repository and reinstall it from there within your website (inside your site, Plugins > Add New, search for Nginx Helper, click install and activate).

## Redis Object Caching Plugin

To reinstall the Redis Object Caching plugin, head over to your Sites page inside your GridPane account and open the website customizer:

Click through to the Caching tab, and then click through to Object Caching. Here you simply need toggle it off and then toggle it back on again. This will reinstall the plugin for you.

## LiteSpeed Cache Plugin

To reinstall the LiteSpeed Cache plugin, you can find this in the WordPress Repository and reinstall it from there within your website (inside your site, Plugins > Add New, search for LiteSpeed Cache, click install and activate).

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

