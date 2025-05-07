# WP Rocket and Rocket-Nginx Caching on GridPane | GridPane

# WP Rocket and Rocket-Nginx Caching on GridPane

 

5 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

All credit for this article belongs 100% to SatelliteWP for their awesome work creating Rocket-Nginx.

Rocket-Nginx is an Nginx configuration for the very popular WP-Rocket plugin. Please see their full guide for a complete and more comprehensive rundown: https://github.com/SatelliteWP/rocket-nginx

Also see their license and warranty info here: https://github.com/SatelliteWP/rocket-nginx/blob/master/license.md

 

 

### Important

The installation instructions in the Github repo may change over time. This article is up-to-date as of 23rd Feb 2022, but please be sure to check for any updates and adjust the settings below accordingly.

## Rocket-Nginx is not supported by GridPane

This is one of those things that we’ve been asked about, but don’t support. This is a use at your own risk deal if you really, really want to use WP Rocket over our server side caching.

That said and out of the way, we’ve been successful in setting this up in our testing, and here is how to set up Rocket-Nginx on GridPane 🙂

Everything that follows below is from the above github by SatelliteWP, except for one small tweak in step 4.

### Step 1. Turn off GridPane caching and install WP Rocket on your website

Be sure to turn off GridPanes page caching inside your websites configuration modal and then run a full cache clear via the self help tools. If you haven’t already, install WP Rocket on your website/s.

### Step 2. SSH into your server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 3. Install Rocket-Nginx

First, navigate to /etc/nginx:

```
cd /etc/nginx
```

And then run:

```
git clone [https://github.com/satellitewp/rocket-nginx.git](https://github.com/satellitewp/rocket-nginx.git)
```

We’ve now cloned in all the files we need to complete our Rocket-Nginx setup into /etc/nginx/rocket-nginx. Next we need to generate the default configuration. To do so, run the following three commands:

```
cd rocket-nginx
```

```
cp rocket-nginx.ini.disabled rocket-nginx.ini
```

```
php rocket-parser.php
```

The above will generate the default.conf configuration that can be included for all websites.

### Step 4. The tweak for GridPane

This part is the only step that differs from SatelliteWP’s installation instructions. We can now either apply this to one specific site, or all sites on the server.

To apply to only one site, create a file called “rocket-main-context.conf in your websites nginx directory with the following command:

```
nano /var/www/site.url/nginx/rocket-main-context.conf
```

Switch out “site.url” for your domain name. E.g.

```
nano /var/www/gridpane.com/nginx/rocket-main-context.conf
```

To apply it to every website on your server you’ll need to edit the main-context.conf in /nginx/extra.d. Open it up with the following command:

```
nano /etc/nginx/extra.d/main-context.conf
```

Now in either our website or servers main-context, copy and paste the following:

```
# Rocket-Nginx configuration
 include rocket-nginx/conf.d/default.conf;
```

Now Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

We now need to test our nginx syntax with:

```
nginx -t
```

If there are no errors present reload nginx with the following command:

```
gp ngx reload
```

Your Rocket-Nginx setup is now complete.

### Step 5. Testing Rocket-Nginx

Head inside your website and clear the WP Rocket cache and let it rebuild with the preload function located at yourwebsite.com/wp-admin/options-general.php?page=wprocket#preload

Then head to your home page in incognito mode and:

A closer look:

In the images above I’ve got a couple of extra options as I’ve turned on debug, but this isn’t necessary.

What we want to know is:

“X-Rocket-Nginx-Serving-Static: Did the configuration served the cached file directly (did it bypass WordPress): Yes or No.”

Yes is what we’re looking for (as shown above). If you got a No, then you can turn on debug below to learn more (and also try refreshing the page and checking again).

### Step 6. Turning on Debug

To turn on debug, we need to open the rocket-nginx.ini file and change the debug value from:

debug = false to -> debug = true

To do this, run the following commands:

```
cd /etc/nginx/rocket-nginx
```

```
nano rocket-nginx.ini
```

Change debug from false to true, and then Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano. Next regenerate your Nginx configuration file by running the parser:

```
php rocket-parser.php
```

Check your nginx syntax with:

```
nginx -t
```

If there are no errors present reload nginx:

```
gp ngx reload
```

This will add the following headers to your response request:

“X-Rocket-Nginx-Reason: If Bypass is set to “No”, what is the reason for calling WordPress. If “Yes”, what is the file used (URL).X-Rocket-Nginx-File: If “Yes”, what is the file used (path on disk).”

Please refer to SatelliteWP’s github and our diagnosing caching issues article for troubleshooting.

Diagnosing Caching Issues

 

## Migrating a Website Using Rocket-Nginx Caching

If you’ve setup Rocket-Nginx caching for your websites (WP Rocket and Rocket-Nginx Caching on GridPane) you will get an Nginx syntax error if you don’t first setup Rocket-Nginx on the destination server, or remove the /var/www/site.url/nginx/rocket-main-context.conf from your website before migrating.

The error will look as follows:

```
root@server-name:~# nginx -t
nginx: [emerg] open() "/etc/nginx/rocket-nginx/default.conf" failed (2: No such file or directory) in /var/www/site.url/nginx/rocket-main-context.conf:2
nginx: configuration file /etc/nginx/nginx.conf test failed
```

Be sure to either remove Rocket-Nginx caching from your website before migrating OR, setup Rocket-Nginx on your destination server before migrating.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

