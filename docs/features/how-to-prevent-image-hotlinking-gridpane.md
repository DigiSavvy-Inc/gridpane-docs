# How to Prevent Image Hotlinking | GridPane

# How to Prevent Image Hotlinking

 

2 min read 

## Introduction

Hotlinking is where someone loads an image from another website on their own website, directly off their server and effectively stealing their bandwidth (and probably also breaking a copyright law by not having the appropriate licensing/permission in many cases).

If you’d like to put protection in place on your website, below will walk you through this process.

### Table of Contents

 

## SSH Into Your Server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Configure Hotlinking Protection on Nginx

### Nginx Step 1. Create Your Nginx Config

We now need to create a config and add our rules to it. To keep things simple, we’ll name it inline what we’re trying to do and call it hotlink-main-context.conf.

To create the file, run the following (switching out “site.url” for your websites domain):

```
nano /var/www/site.url/nginx/hotlink-main-context.conf
```

Example:

```
nano /var/www/gridpane.com/nginx/hotlink-main-context.conf
```

Next, paste the following inside the file (again replacing site.url with your domain):

```
location ~ .(gif|png|jpe?g|svg)$ {
 valid_referers none blocked site.url *.site.url;
 if ($invalid_referer) {
 return 403;
 }
}
```

Ctrl+O and then press enter. Then Ctrl+X to exit nano.

 

### Nginx Step 2. Check Your Syntax and Reload Nginx

We now need to test our nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

Your website is now protected against hotlinking!

 

## Configure Hotlinking Protection on OpenLiteSpeed

To edit your sites .htaccess file, use the following command (switching out site.url with your site URL):

```
nano /var/www/site.url/htdocs/.htaccess
```

Add the following to the file:

 

```
# Check for the specified image extensions
RewriteCond %{REQUEST_URI} \.(gif|png|jpe?g|svg)$ [NC]

# Check for invalid referrers
RewriteCond %{HTTP_REFERER} !^$
RewriteCond %{HTTP_REFERER} !^https?://(www\.)?%{HTTP_HOST}/ [NC]
RewriteCond %{HTTP_REFERER} !^https?://%{HTTP_HOST}/ [NC]

# Return a 403 Forbidden response
RewriteRule .* - [F]
```

Next, save the file with CTRL+O and then Enter, and exit nano with CTRL+X.

You’re all set.

GridPane OpenLiteSpeed actively monitors .htaccess files for all of your sites using a file modification-based daemon and will take care of OLS reloads for you automatically.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

