# Why Does My Website “Download” Instead of Load? Double Gzip and How to Fix it | GridPane

# Why Does My Website “Download” Instead of Load? Double Gzip and How to Fix it

 

2 min read 

## The Problem

If you’re trying to access your website, but instead it downloads instead of loading in the browser, the issue is caused by the GZIP compression being enabled twice.

GZIP is enabled by default on GridPane servers, however, some plugins have an option to enable GZIP as well.  If a plugin doesn’t check the server’s GZIP compression status and compresses the files anyway, it results in a doubled up compression. In this state, the file isn’t readable by the browser and instead downloads it as a blob.

 

## The Fix

We haven’t many cases of this issue, and so far I’m only aware of the WP Rocket plugin being the cause. You can fix this via their helper plugin, clear your cache, and then the website should load correctly again on both Nginx and OpenLiteSpeed.

On OpenLiteSpeed, you may also need to remove any added setting to the .htaccess file. WP Rocket and other plugins should remove the helper plugin is installed/configured, but if you find that your site still downloads even after clearing the cache, you’ll need to check and fix this.

### The .htaccess Location

The .htaccess file is a hidden file located inside your websites /htdocs directory.

To view it, you’ll first need to connect to your server. If this is your first time doing so, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Editing Your .htaccess File

You can edit the file within nano with the following command (replace site.url with your website URL):

```
nano /var/www/site.url/htdocs/.htaccess
```

Clear out the configuration the plugin has added, and then you can save the file with CTRL+O followed by Enter. You can then exit nano with CTRL+X.

Now regenerate your vhost with (again replacing site.url with your website’s URL):

```
gpols site site.url
```

Clear your site’s cache and check the page again. Your site should now load correctly.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

