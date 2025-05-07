# Exclude a Page or Cookie from Nginx Server Caching | GridPane

# Exclude a Page or Cookie from Nginx Server Caching

 

6 min read 

## Introduction

If you’re building projects for your clients, or you’re managing a website that has some complex functionality, you may find that you need a page to be excluded from the cache for it to work correctly.

This article will walk you through how to set this up with GridPane’s Nginx server caching options, and how to make cache exclusions for individual websites or all websites on a server.

### Table of Contents

Before we begin, be sure to confirm which cache type you’re using inside of your website’s customizer by heading to your Sites page inside your GridPane account and clicking on your site’s domain name.

 

 

### Alternative Method: Exclude Pages with PHP Headers

You can also use PHP Headers to create custom cache exclusions, and control this directly within your WordPress websites. To learn more, check out this article: 
Using PHP Headers to create custom cache exclusions

## Step 1: Connect to your server

Use your favorite SSH client and connect to your server IP as root. If this is your first time connecting to one of your servers, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2.1: Create your page excludes

Creating cache exclusions is a relatively simple process. Below we’ll look that the different types of exclusions you can create.

NOTE: The following needs adding to your server inside either a website-specific config or a server-level config as detailed in steps 2.1 and 2.2 below this section.

### Exclude a Single page

Below shows the basic structure for making page exclusion, and you simply need to switch out “/examplepage/” with your desired page:

```
if ($request_uri ~* "(/examplepage/)") {
 set $skip_cache 1;
 set $skip_reason "${skip_reason}-request_uri";
}
```

If the page is served with both trailing slash (site.url/examplepage/) and non-trailing slash (site.url/examplepage), you should modify the condition with an asterisk to cater both cases like this:

```
if ($request_uri ~* "(/examplepage.*)") {
```

You can also give a specific reason, by switching out “${skip_reason}” with the reason you’re excluding this page. For example:

```
set $skip_reason "login-request_uri";
```

### Exclude Multiple Pages

You can exclude multiple pages from the cache like this:

```
if ($request_uri ~* "(/examplepage/|/another-page/|/third-page/)") {
 set $skip_cache 1;
 set $skip_reason "${skip_reason}-request_uri";
}
```

### Wildcard Exclusions

If you want to exclude a parent page plus all child pages, or an entire CPT (or whatever your use case), you can create a wildcard exclude like this:

```
if ($request_uri ~* "(/parent-page.*)") {
 set $skip_cache 1;
 set $skip_reason "${skip_reason}-request_uri";
}
```

### Targeting the Homepage

Targeting the homepage isn’t intuitive at first glance and use cases for it are rare (generally it is the most visited page of any website so it is better cached whenever possible). If you do need to exclude the homepage, here is how to specifically target it:

```
if ($request_uri ~ ^/$) {set $skip_cache 1;set $skip_reason "${skip_reason}-your_cookie";}
```

The dollar sign $ is important here as signals the end of the string and ensures that all of your other pages don’t match the rule.

 

## Step 2.2: Create your cookie excludes

This is more advanced, but useful for developers who have specific use cases where adding each page individually / having to update this regularly could be better handled by setting cookies on specific pages instead.

Follow the same steps as above, but instead of adding a page specific exclusion, use the following code block to add a cookie exclusion:

```
if ($http_cookie ~* "your_cookie_name") {set $skip_cache 1;set $skip_reason "${skip_reason}-your_cookie";}
```

For example, to exclude the SEOPress user consent cookie you can use the following:

```
if ($http_cookie ~* "seopress-user-consent-accept") {set $skip_cache 1;set $skip_reason "${skip_reason}-http_cookie";}
```

 

## Step 3.1: Exclude your pages and/or cookies for an individual website

Now inside your server, we need to add our page exclusions. Be sure only to use the correct command below for the type of page caching you’re using. Adding our exclusion to the wrong caching method will have no effect.

Redis: If you’re using Redis page caching, enter the following and hit enter (replacing site.url with your domain name):

```
nano /var/www/site.url/nginx/custom-skip-redis-cache-context.conf
```

FastCGI: If you’re using FastCGI page caching, enter the following and hit enter (replacing site.url with your domain name):

```
nano /var/www/site.url/nginx/custom-skip-fcgi-cache-context.conf
```

Then paste exclusion inside your SSH client. On most machines, this will be a right-click with your mouse, not a CTRL + V.

```
if ($request_uri ~* "(/examplepage/)") {
 set $skip_cache 1;
 set $skip_reason "${skip_reason}-request_uri";
}
```

Now just hit CTRL + X on your keyboard, and it will ask if you want to save, click Y to save. Head to step 4 below.

 

## Step 3.2: Exclude your pages and/or cookies for all websites on a server

The process for excluding a page for all websites is similar to what we described above in part 3.1 – the exclusion itself follows the same format. However, instead of saving the include in the site-specific Nginx directory (/var/www/site.url/nginx), we’ll create and save a file in the following directory:

```
/etc/nginx/extra.d
```

You can name the file in one of the following ways:

Adding our exclusion to the Redis-specific config will have no effect on sites that use FastCGI, and vice versa.

### Create the file

Create the appropriate file for your use case with nano. For example:

```
nano /etc/nginx/extra.d/exclude-name-skip-redis-cache-context.conf
```

Then paste exclusion inside your SSH client. On most machines, this will be a right-click with your mouse, not a CTRL + V.

```
if ($request_uri ~* "(/examplepage/)") {
 set $skip_cache 1;
 set $skip_reason "${skip_reason}-request_uri";
}
```

Now just hit CTRL + X on your keyboard, and it will ask if you want to save, click Y to save.

### Copy the file into extra.d/_custom

After adding the include, make sure to copy the include to this folder:

```
cp /etc/nginx/extra.d/exclude-name-skip-redis-cache-context.conf /etc/nginx/extra.d/_custom/exclude-name-skip-redis-cache-context.conf
```

This will ensure that your settings will persist through Nginx configuration updates.

 

 

### IMPORTANT

If you migrate a website to another server, a server-wide configuration file like we've detailed here will not be migrated along with it, so you will need to set your exclusion up again on the new server.

## Step 4: Check and Reload Nginx

Check the Nginx configuration file with:

```
nginx -t
```

This will test your configs. If it shows any failures, or any message other than what is below, do not proceed to reload Nginx.

If no errors are returned, reload Nginx with:

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

