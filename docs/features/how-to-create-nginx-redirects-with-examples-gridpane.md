# How to Create Nginx Redirects (with Examples) | GridPane

# How to Create Nginx Redirects (with Examples)

 

8 min read 

## Intro

Sometimes you might need to do different kinds of redirects that aren’t quite covered by our normal redirects. In this article, we’ll look at several redirect examples, and add to them over time.

### Table of Contents

 

## Getting Started

To set up Nginx redirects you will first need to SSH into your server. To get started, please see the following articles:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

 

### Important

Please note that editing any of the files located here: 
/etc/nginx/sites-available/
Will get overritten at some point as there are many functions that will trigger the refreshing of these files. We add a "Do not edit directly" warning to the specific configs that are subject to change or that could cause potential stack issues when editing directly.

## Let’s Encrypt and Redirects

The following applies to examples 2 and 3 of this article.

One of the challenges that comes with redirects that point to another domain is that once they’re in place, by default, when Let’s Encrypt requests access to the .well-known directory the request is redirected away and it cannot confirm domain ownership. Without this, your website is not considered eligible for either a new SSL or an SSL renewal if you’re using the webroot method.

### Primary Domain Redirects

To ensure that your domain’s SSL can provision/renew if you’re not using our DNS API integrations, we need to ensure that Let’s Encrypt can still access the .well-known directory once the redirect is in place.

To do this, we have the following in our configs:

```
location ~ /\.well-known {
allow all;
include /var/www/${primary_site}/nginx/*well-known-${primary_domain}-context.conf;
include /var/www/${primary_site}/nginx/*well-known-context.conf;
}

include /var/www/${primary_site}/nginx/*-main-${primary_site}-context.conf;
```

### Alias Domain Redirects

To ensure that your Alias domain’s SSL can provision/renew if you’re not using our DNS API integrations, we need to ensure that Let’s Encrypt can still access the .well-known directory once the redirect is in place.

To do this, we have the following in our configs:

```
location ~ /\.well-known {allow all;include /var/www/${primary_site}/nginx/*well-known-${add_on_domain}-context.conf;include /var/www/${primary_site}/nginx/*well-known-context.conf;}include /var/www/${primary_site}/nginx/*-main-${add_on_domain}-context.conf;
```

### Summary

The above includes mean that we can allow requests to the .well-known directory to take place before the includes where we add our redirect. With this, Let’s Encrypt can verify your domain correctly.

 

## 1. Regular Nginx Redirects

Regular redirects are pretty straightforward with GridPane. We also have this dedicated KB article if you happen to be using the Redirection plugin:

Redirection Plugin: How to export redirects and set them via Nginx

### Step 1. Create redirect-main-context.conf

We can add redirects via the *-main-context.conf include.

First, we need to create a file called redirect-main-context.conf inside /var/www/site.url/nginx. Create the file with the following command (switching out site.url for your domain name):

```
nano /var/www/site.url/nginx/redirect-main-context.conf
```

Next add your rewrites. The format order is as follows:

Putting it all together:

```
rewrite ^/example-uri$ /destination-uri permanent;
```

Add you rewrites to your config. Multiple redirects can be added like so, one per line:

```
rewrite ^/example$ /sample-page permanent;
rewrite ^/another-example$ https://domain.com permanent;rewrite ^/cart$ /basket permanent;
```

Now Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

### Step 2: Check and reload Nginx

Finally, we need to check if the conf files are correct then reload Nginx.

Test your nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

 

## 2. Old Domain to New Domain

This can be particularly useful if you’re redirecting full requests for existing site old-domain.url to new site new-domain.url, if on a different servers.

Let’s assume you want to redirect all traffic from an existing site with an old domain to a new site, with the full request URI.

If both sites are on the same server, it’s as simple as adding the old domain to the site as a redirect 301 domain via our domains manager and swapping DNS.

But, if that old site still exists on another server and you want to keep that site up AND the DNS resolving to the old server, you can use one of our Nginx includes.

 

### Step 1. Create the .well-known Config

We need to create 2 configs to set this redirect up and have it work with Let’s Encrypt. The first is the .well-know config as follows:

```
/var/www/{primary.domain}/nginx/well-known-main-context.conf
```

Create the file with the following command, switch out site.url with your domain name:

```
nano /var/www/site.url/nginx/well-known-main-context.conf
```

Add the following to file:

```
location ~ /\.well-known {allow all;}
```

Next press CTRL+O to save the file, followed by Enter. Close nano with CTRL+X.

### Step 2. Create the Redirect Config

Run the following command to create the redirect configuration file, switching out site.url for your domain:

```
nano /var/www/site.url/nginx/redirect-root-context.conf
```

Add your redirect in the following format, switching out new-domain.url for the domain of the website you want to redirect to:

```
return 301 https://new-domain.url$request_uri;
```

### Step 3. Check and reload Nginx

Test your Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

 

## 3. Redirecting olddomain.com to newdomain.com/something

This example and the one that follows below instead make use of an alias domain to setup a redirect that is different to standard 301 redirect.

E.g. Directing olddomain.com > newdomain.com/en/

 

### Step 1. Add your alias domain

Add the domain you want to redirect as an alias to your primary domain that you want it to redirect to.

### Step 2. Setting your redirect

Inside your vhost you have this include (site.url = your domain name):

```
include /var/www/site.url/nginx/*-main-aliasdomain.url-context.conf;
```

So, using our example above, inside your server you could create the following inside your primary sites /nginx directory:

```
nano /var/www/primarydomain.com/nginx/redirect-main-aliasdomain.com-context.conf
```

And then add the following location block and your redirect:

```
location ~ /\.well-known {
allow all;
}

location ~ / {
return 301 https://primarydomain/en$request_uri;
}
```

CTRL+O and then Enter to save the file, and then CTRL+X to exit nano.

NOTE: The tilde ~ here is important because the exact root location match exists already in the primary domains configs that the alias shares. If you dont use ~ then you will hit an Nginx syntax error in the next step.

### Step 3: Check and reload Nginx

Test your nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

You’re all set!

 

 

### Note

Please note this will require an updated config, any alias domains configs updated since May 3rd 2021 will have these includes, however any older config that hasn't been regenerated recently will not. We do not automatically replace in-place configs. The domain action such as changing www/root routing, or site actions such as changing cache types will regenerate any pre-existing config files to the latest version.

## 4. Redirecting olddomain.com/something to newdomain.com/somethingelse

Scenario 2: Inside of GridPane, you have the site “newdomain.url“.

You want to have any requests for your olddomain.url/something to redirect to newdomain.url/something-else.

### Step 1. Add “olddomain.url” as an alias

Add the old domain olddomain.url as an alias inside the domains tab of newdomain.url site.

### Step 2. Setting your Redirect

On your server create the following file:

```
/var/www/newdomain.url/nginx/redirects-main-olddomain.url-context.conf
```

Inside that file add the following:

```
location /something {
    rewrite ^(.*)$ https://www.newdomain.url/something-else redirect;
}
```

### Step 3: Check and reload Nginx

Test your nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

 

## Redirect Without Multiple Redirects

The main-context.conf adds the redirect within the HTTPS main context.

If you need to go straight from http://website.com to https://www.othersite.com, this can be done using either the *-return-https-context.conf if your routing is set to None or root, or the *-return-www-context.conf if your site is set to www. These take place before the main-context.

### Step 1. Create Your Configuration file

Here we need to create a file called redirect-return-https-context.conf or redirect-return-www-context.conf inside /var/www/site.url/nginx.

Create the file with the following command (switching out site.url for your domain name) if the site your site’s routing is set to None or root:

```
nano /var/www/site.url/nginx/redirect-return-https-context.conf
```

If your site is using www routing, create the following:

```
nano /var/www/site.url/nginx/redirect-return-www-context.conf
```

### Step 2. Add your redirect/s

You can formulate your redirects using the examples above and add them to the file.

You can also target specific URI’s like so:

```
if ($request_uri ~* "(/my/page/)"){return 301 https://www.newsite.com/new-page/ ;}
```

### Step 3. Check and Reload Nginx

Test your Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

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

