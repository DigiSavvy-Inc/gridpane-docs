# Diagnosing Redirect Issues | GridPane

# Diagnosing Redirect Issues

 

9 min read 

## Introduction

Undesired redirects can be frustrating to deal with. Fortunately, narrowing down the root cause of these issues can usually be done quickly when you know what to check. This article will walk you through the checks for 3 different scenarios:

You may also want to check your site over at the following link to see if it offers any immediate insights:https://www.redirect-checker.org/index.php

Some of these steps may require connecting to your servers. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Your website is redirecting to different site or an internal page, or has a redirect loop

### 1. Clear the Cache

Inside your websites customizer in the caching tab and recheck your website – ideally in incognito mode as detailed below.

### 2. Check the Website in Incognito Mode

Check the site in an incognito window to rule out a browser issue with cookies or caching. If the site works correctly, clear your website’s browser cache.

### 3. Does the website have a Valid SSL?

If your website is loading over HTTPS but doesn’t have a valid SSL this can manifest in a few different errors. SSL related errors are much easier to pin down. Please see the troubleshooting steps in this counter-part article that details symptoms and causes for these errors:

Why do I see a different site than I’m supposed to, an SSL warning, signon.php, or too many redirects?

The above article covers the following:

Number 1 is caused by Cloudflares flexible SSL setting, and 2, 3 and 4 are all easily solved by provisioning an SSL certificate.

### 4.1 Are The Database SITEURL and HOME Settings are incorrect?

If you’re being redirected to staging or a previous URL and routing for your domain is set to “None” (and not “root” or “www”), then you may have the incorrect address set within the database inside the wp_options table.

Previously, we used to strictly control these values. but so that third-party services such as Cloudflare APO, we now only control these values is when you specifically set either the root or www route type.

You can learn more about routing here:Manage Site Domains and Site Routing (non www vs www)

To check, head to the Sites page inside your account, and open up PHPMyAdmin for your website by clicking the database icon:

Click through to the wp_options table:

Here make sure your siteurl and home are set correctly. If you need to edit them, simply click on the incorrect link to edit, and then press Enter when it is correct.

### 4.2 If it’s a multisite, check the wp_blogs table

If you’ve changed domains on a multisite, be sure to check the wp_blogs table.

### 5. Newly migrated website? Check for Two competing wp-config.php files

If things aren’t working the way they’re supposed to after migrating, and the above issues aren’t the cause, make sure that there isn’t a second wp-config.php file inside your websites /htdocs folder.

GridPane securely stores the wp-config.php file 1 level up outside of /htdocs here:

```
/var/www/site.url
```

If you have two wp-config.php files – 1 in the correct place, one in /htdocs – these can interfere with each other and cause problems. Please simply delete the wp-config.php file inside /htdocs if it exists, and leave ours in its place.

You can do this either by connecting to your server by SSH (links at the beginning of the article), or by connecting to your server over SFTP:

Connect to a GridPane Server by SFTP as Root user

To  delete them directly on your server,

you can navigate to your websites htdocs folder with the following command (switching out “site.url” for your websites domain name):

```
cd /var/www/site.url/htdocs
```

Then display the contents of the file with:

```
ls -l
```

And if you see a wp-config.php file, you can rename it with:

```
mv wp-config.php wp-config.php_off
```

Or you can delete it with:

```
rm wp-config.php
```

Once that’s done you’re all set!

### 6. Is there an Nginx configuration or .htaccess rule in place?

If you have migrated your website and you previously had a redirect setup in either an Nginx configuration file or .htaccess, then these settings will have carried over. Check and remove the redirects, then reload Nginx/OpenLiteSpeed.

### 7. Check Your DNS/CDN Configuration

Do you have any custom rules set up at your DNS provider or CDN that could be causing the redirect?

If you disable the Cloudflare proxy or your CDN, does the issue persist? You can also test this by bypassing them with a local redirect:

How can I edit my local hosts file to redirect URLs

Deactivating these will be necessary during an ongoing support ticket.

### 8. Do Permalinks need a refresh/reset?

We’ve seen migrations where the permalink settings have been changed. Check your settings are correct, re-save them, then clear the whole cache. Does this fix the issue?

You can flush your permalinks with the following command (replace site.url with your websites URL):

```
gp wp site.url flush permalinks
```

Then clear the cache either inside the UI or with this command:

```
gp fix cached site.url
```

### 9. Check Your Plugins

At this point, it’s almost certainly a plugin within your website.

If you deactivate all plugins (rename the plugin directory via SSH or SFTP) does this fix the issue? If yes, rename the folder back to “plugins” and deactivate them one by one until you find the culprit.

 

## Your website is redirecting all pages to wp-login.php

### 1. Check the Website in Incognito Mode

Check the site in an incognito window to rule out a browser issue with cookies or caching. If the site works correctly, clear your website’s browser cache.

### 2. Is the Force Login plugin active?

Have you migrated your website or pushed from staging to live? Check your website for Force Login plugin. Though rare, it’s possible that this failed to remove during the push. If you’ve migrated a different way (manually or via a plugin), then this will need deactivating.

Once deactivated, the redirect should disappear.

 

## Your website is redirecting back to the wp-login.php after logging in

If you’re unable to login, check the following:

 

## Your website is redirecting to wp-admin/setup-config.php

This redirect occurs when the WordPress can’t find the wp-config.php file (which can be caused by a few different things). We’ve only seen this issue come up once on support, and below are the possible scenarios that we’re aware of.

### 1. Reset Your Permissions

Incorrect permissions are the most likely cause for this error. Head to the Tools page inside your account and run a permissions reset:

### 2. Check Your Database

Check your websites htdocs folder. Is there an additional wp-config.php file? If yes, remove it or rename it.

### 3. Clear your cache

Clear both the website cache and your browser’s cache (or check in incognito).

 

## Specific files are experiencing “too many redirect” errors

In one case in support, we saw a self-hosted (uploaded to the uploads directory) video background, that was failing to load, reporting “too many redirects” as the console error.

Pasting the file path for that video into the Redirect Checker website revealed that this was a 302 taking place within WordPress.

The root cause ended up being an Nginx configuration that had been put in place for MemberPress, which has this line, putting rules in place that affect these file formats:

```
location ~* \.(zip|gz|tar|rar|doc|docx|xls|xlsx|xlsm|pdf|mp4|m4v|mp3|ts|key|m3u8)$ {
```

In this case it was an .mp4 file, which we edited out of this line. After saving the file and reloading Nginx, the video began to work correctly again.

Check your Nginx folder and any configs that you have manually added in /var/www/site.url/nginx.

If you’re unsure, you can send a ticket in to support with all the details – the error, the file, the website page, and the configs, and we can let you know if anything there might be responsible.

 

## 307 redirects

At the time or writing 307 redirects only appears to happen inside Chromium based browsers.

When one your websites is loaded via HTTPS in your browser the following security header is set:

```
Strict-Transport-Security: max-age=31536000
```

This header tells the browser to only load the HTTPS version of a site. More details here:https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security

On Chrome this setting is cached when the server makes the first HTTP request.

This is why on the first request you’ll get the 301 redirect. If an HTTP request is made once again Chrome remembers the cached setting and internally redirects (redirect 307) to the HTTPS version. Chrome does this to reduce the number of requests that have to be made to the server thus loading the site faster.

### If Your SEO Agency is Making a Fuss About It Even With the Above Info…

Although this is not recommended, you can set the HSTS header to 0 thus forcing the browser to make the round trip to the server and return 301.

This is how you can set this up:

1. Log into your server via SSH as root

2. Run the following:

```
nano /etc/nginx/common/headers-https.conf
```

Here you can set the Strict-Transport-Security value to 0:

```
more_set_headers "Strict-Transport-Security: max-age=0" always;
```

Save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

3. Next check the Nginx conf syntax with:

```
nginx -t
```

If everything is ok then reload Nginx with:

```
gp nginx reload
```

 

## Site redirects when Cloudflare proxy is active (orange clouds ON)

If you’re seeing that your website redirects when you turn the Cloudflare proxy on (orange clouds active), and then the redirect stops once you turn it off (grey clouds), then your domain was likely previously registered with a Cloudflare SaaS partner.

Technically, what’s happening is not actually a redirect, it’s Cloudflare pointing the domain to the A record of the previous SaaS partner.

Learn more about this issue and how to resolve it in this knowledge base article:

Website Redirecting When Cloudflare’s Proxy Active (Orange Clouds ON)

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

