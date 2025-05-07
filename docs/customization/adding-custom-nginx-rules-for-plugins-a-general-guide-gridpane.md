# Adding Custom Nginx Rules for Plugins - A General Guide | GridPane

# Adding Custom Nginx Rules for Plugins – A General Guide

 

4 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

## Introduction

Some plugins require custom configurations to be added to Nginx servers in order for them to function correctly.

This article will explain how to add your plugin configurations using our main-context.conf includes, which is considered to be anything within the Server {} block of a given site.

Please note that if they require you to add code to a place other than the server directive/block, please post in the community forum for assistance, and we will look at creating a dedicated article for that plugin.

### Existing Articles

We already have articles for the most popular plugins we know of:

For SEO plugins, we have default includes out of the box, so no additional configuration is needed. This covers Yoast, Rankmath, and SEOPress. There are no SEO plugins that we’re aware of that don’t work out of the box on GridPane.

Let’s get started.

 

## Step 1. SSH into your server

To implement these rules you will need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Choose Your Config Location

You can add your Nginx rules to apply to every site on your server or just one specific site. We use the following includes:

```
include /etc/nginx/extra.d/*main-context.conf;include /var/www/site.url/nginx/*-main-context.conf;
```

### Site-Specific

In most cases, you’ll only want your config to apply to one specific site. Here we can use:

```
/var/www/site.url/nginx/pluginname-main-context.conf
```

To apply this, follow Step 3A below.

### Server-wide

If you want your configuration to apply to ALL of the sites on your server, you can add them here:

```
/etc/nginx/extra.d/pluginname-main-context.conf
```

To apply this, follow Step 3B below.

### Naming Your Config

To keep things organized and easy to identify at a glance, we recommend that you name the file with the plugins name, for example: myplugin-main-context.conf.

The wildcard * at the beginning of the above includes can be replaced with whatever makes sense for you.

 

## Step 3A. Create a Server-Wide Config

For ALL sites on your server, you can create your config with the following command (customize the “myplugin” as you see fit):

```
nano /etc/nginx/extra.d/myplugin-main-context.conf
```

This will both create the file and open it with the nano editor ready for the next step.

Next, paste your code into this file:

```
Paste plugin configuration
```

You can now hit Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

To finish up, copy the file over to the /_custom directory with (again replacing the config name):

```
cp /etc/nginx/extra.d/myplugin-main-context.conf /etc/nginx/extra.d/_custom/myplugin-main-context.conf
```

 

## Step 3B. Create a Site-Specific Config

For a specific site, you can create your config with the following command (switching out “site.url” for your website’s domain and customize the “myplugin” as you see fit):

```
nano /var/www/site.url/nginx/myplugin-main-context.conf
```

This will both create the file and open it with the nano editor ready for the next step.

Next, paste your code into this file:

```
Paste plugin configuration
```

You can now hit Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

 

## Step 4. Check and reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

