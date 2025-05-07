# Updating the GridPane Redis Object Cache Forked Plugin Back to the Original Plugin | GridPane

# Updating the GridPane Redis Object Cache Forked Plugin Back to the Original Plugin

 

3 min read 

### Table of Contents

 

## Introduction

For the last couple of years, GridPane has used a fork of the Till Kruss Redis Object Cache plugin. This was due to some compatibility issues which have since been resolved.

As of August 19th 2022, we have now switched back to the original plugin that can be found in the WordPress repo. This is the object caching plugin that will now be installed on newly created websites moving forward.

Any existing sites that use our fork will continue to work, however, we do recommend that you update your sites at some point in the near future. This article details several methods for how to do this.

 

## Method 1. Toggle Object Caching OFF and then back ON

If you toggle off Redis Object caching inside your website’s customizer, then the old GridPane forked plugin will be dropped, and Till’s plugin will then be installed and the drop-in updated.

This needs to be done on a per-site basis. Method 2 below allows for mass updating your sites.

 

## Method 2. Update Using a Token File

This method allows you to update your sites in 2 ways:

### How it Works

This will only attempt the update your websites if the token is empty, or the token contains the site URL, AND if our plugin is found.

It then runs through a sequence to flush the cache, uninstall our plugin, install the new plugin, update drop-in and flush the cache again, and then add the config value to disable the plugin’s ads.

You’ll need to connect to your server to implement this method. If this is your first time, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Option 1. Update ALL Sites

To update ALL websites on your server you simply need to copy and paste the command below. This will create a token file that will automatically update all of your websites when our daily worker runs, which is usually set to run overnight.

Create the token file with:

```
touch /root/update.object.cache.plugins
```

Once you’ve copied and pasted the above our systems will do the rest. Check your websites tomorrow and you should be all set.

 

### Option 2. Selectively bulk update specific sites

If you’d prefer to update only specific sites or update in batches, you can do this by adding the site URLs to this token file.

If the file is empty, it will update all sites, but if the file contains URLs, it will only update these specific sites.

Create the file with the following command which will also open up the nano editor:

```
nano /root/update.object.cache.plugins
```

Add your sites, 1 per line, and using only the URL, don’t include https:// or www. For example:

```
mywebsite.comstaging.mywebsite.comsomeotherwebsite.net
```

Once you’ve added all of the websites that you want to update, save the file with CTRL+O and then Enter. Exit nano with CTRL+X.

You’re now all set, and our systems will update your sites the next time our daily worker runs. Check your websites tomorrow.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

