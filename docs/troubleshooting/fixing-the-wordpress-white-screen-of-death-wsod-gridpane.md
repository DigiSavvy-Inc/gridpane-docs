# Fixing the WordPress White Screen of Death (WSOD) | GridPane

# Fixing the WordPress White Screen of Death (WSOD)

 

3 min read 

WSOD is something that rarely ever happens, but when have seen it, it’s almost always related to caching, and usually when there are 2 types of caching working on top of one another. Other causes for this error are rare on GridPane, but we will cover all of them below.

We recommend you begin your troubleshooting by checking your cache.

## First, check your cache

If you’re experiencing a WSOD, you can quickly check if this is caching-related by adding a query string to your URL.

Example: gridpane.com/?123

This will BYPASS the cache, loading your website from scratch. If your website loads correctly without the cache, then you’ve identified the cause of the problem.

If you have a caching plugin installed (WP Rocket, Swift, Breeze, Super Cache, etc), then you may need to disable caching on GridPane by toggling it off inside your website configuration modal. Next, run a full cache clear via the Site Customizer > Caching tab:

Or on the self-help tools page as pictured below:

Regular caching plugins are not compatible with GridPane’s native server caching. You will need to choose between our caching and your plugin – we recommend our caching.

## Check for a failed WordPress update

Check your website’s htdocs folder either via SSH or SFTP. Is there a .maintenance file there? If yes, delete this and recheck your website. You may need to clear the cache as shown above.

If checking by SSH, you can navigate to your htdocs folder with the following command (replacing “site.url” with your domain name):

```
cd /var/www/site.url/htdocs
```

Check for the .maintenance file with:

```
ls -l
```

If this file exists, you can remove it with:

```
rm .maintenance
```

## Turn on WP_DEBUG and Check your Nginx Error Log

Open up your website configuration modal and navigate through to the logs tab. Here you first want to check your Nginx Error log to see if you can quickly spot what’s going wrong.

If you can’t spot the error, turn on Debug for your website:

We have an article detailing WP_DEBUG here:

WordPress Debug and Query Monitor

### Test your plugins

If you spot an issue with a plugin, you can deactivate it and then check the site again.

If you’re unable to log in, try renaming your plugins folder. To do this, connect to your server via SFTP and rename it from “pluginname” to something like “pluginname-test”. Now retest your website. Has this solved the problem?

If no, change the folder’s name back.

Next, try renaming the entire plugins folder from “plugins” to “plugins-test”. Does this fix the issue?

If yes, then rinse and repeat with each of your individual plugin folders until you find the cause. You can change their name’s back once you’ve identified the problematic plugin.

### Test your theme

If plugins aren’t the cause, try changing themes. If you can’t access your site, simply rename your themes folder from “themename” to “themename-test”. WordPress should default to the latest standard theme. If you don’t that installed, you can upload it via SFTP.

## Increase the WP_MEMORY_LIMIT

By default, GridPane sets the memory limit on new installs at 256M. You may wish to try 512M to see if the fixes the issue for you. You can change this inside your website customizer or via GP-CLI.

### Site Customizer > PHP Tab

Click on the name of your website inside your Sites page to open up the site customizer, and then click through to the PHP tab. Here you’ll be shown your PHP INI settings, and you can update your Memory Limit:

### GP-CLI

SSH into your server and run the following command:

```
gp stack php -site-mem-limit {integer} {site.url}
```

Example:

```
gp stack php -site-mem-limit 512 gridpane.com
```

Recheck your website. If this doesn’t you may want to reach out to support – let us know the website, server IP, and what you’ve done so far.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

