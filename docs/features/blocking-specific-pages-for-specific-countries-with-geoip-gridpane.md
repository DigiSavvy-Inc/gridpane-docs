# Blocking Specific Pages for Specific Countries with GeoIP | GridPane

# Blocking Specific Pages for Specific Countries with GeoIP

 

6 min read 

 

### IMPORTANT

This article is specific to Nginx. We will release an article for OpenLiteSpeed in the future.

## Introduction

In this article, we’ll look at how to block access to specific pages for specific countries. An example use case for this was brought up in our Facebook group where a WooCommerce stores was being targeted with malicious checkout attempts.

One way to deal with this would be simply redirect the stores checkout page to a different page, which you can learn how to do in this article:

Country-Specific Redirects with GeoIP

Another way is to deny access to those pages, which is what we’ll look at below.

### Table of Contents

Before we begin, this is just one of many methods available for implementing Geo-specific redirects. There are WordPress plugins available, and Cloudflare also offers this capability and is actually what we would normally recommend here if possible. If you need more advanced capabilities, [Geo Targetly](https://geotargetly.com/) may be worth a look. 

## 1. Create a Maxmind Account

The ngx_http_geoip2_module that we will be using creates variables with values from the maxmind geoip2 databases based on the client IP (default) or from a specific variable (supports both IPv4 and IPv6). Using this module you can easily filter traffic by a clients GeoIP based on country or city. Find out more here.

The GeoIp2 module makes use of the free GeoLite2 databases that are available from Maxminds website. If you don’t already have one, you can sign up for your account here.

### Activation

The details you need are your Maxmind AccountID + Maxmind License Key.

To activate this on your server, enter the following command, replacing “{account.id}:{license.key}” with your details:

```
gp stack nginx geoip -on {account.id}:{license.key}
```

Example:

```
gp stack nginx geoip -on 57679:sd8Hj7kl
```

The Maxmind account information is only required when you first enable GeoIP2. We autogenerate a maxmind config at /etc/GeoIP.conf and store your account details in the server ENV so any subsequent reenabling can use these stored values. The account details allow the maxmind databases to be updated by a weekly cron.

You can also block specific countries with our available GeoIP2 GP-CLI. Learn more here.

 

## 2. Prepare Your Country Code/s

To implement your redirect you will need the country codes for the specific countries you wish to set things up for.

You can find a list of all available country codes here over on the maxmind website:

ISO 3166 Country Codes

Copy the codes you wish to use.

 

## 3. SSH into Your Server

You will need to SSH into your server to setup your redirects. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## 4. Blocking Pages

To block access to specific pages, we’re going to be returning a 403 Forbidden error.

We’ll do this by setting up our country info, and then using location blocks we’ll target specific URIs and block access to them.

### Step 1. Map Our Target Countries

First we’ll create a configuration called geo-mappings.conf inside /etc/nginx/conf.d:

```
nano /etc/nginx/conf.d/geo-mappings.conf
```

In this example, I’ll be blocking traffic from all countries except for the US and Canada. We can then map our countries like so:

```
map $geoip2_data_country_code $block_checkout_country {
   default yes;
   CA no;
   US no;
}
```

### Step 2. Block Our Pages

We can now use the *-main-context.conf include to create our site specific page blocks. This goes here /var/www/website.com/nginx/*-main-context.conf.

Create the file with:

```
/var/www/site.url/nginx/geo-block-pages-main-context.conf
```

Using the map we created in step 1, we can target all countries except for the US and Canada by specifying that $block_checkout_country = “yes“.

```
location /checkout/ { 
if ( $block_checkout_country = "yes" ) { 
return 403; 
} 
try_files $uri $uri/ /index.php?$args; 
}
```

Save the file with CTRL+O and then Enter. Exit with CTRL+X.

### Customising Further

Using location /checkout/ in the above example also targets all other pages that start with /cart/. For example, this would also return a 403 for website.com/checkout/thank-you.

To specify an exact match, we can use: location = /checkout/.

To specify more than one URI, simply add an additional location block to the file for each like follows:

 

```
location /checkout/ { 
if ( $block_checkout_country = "yes" ) {
 return 403; 
} 
try_files $uri $uri/ /index.php?$args; 
}

location /cart/ {
if ( $block_checkout_country = "yes" ) {
return 403;
}
try_files $uri $uri/ /index.php?$args;
}
```

## How it all Works

This is a good opportunity to learn a little about how all of the above works on your Nginx server.

### How the Map Module Works

When we created our geo-mappings.conf file, we created a variable for the GeoIP country code module, and we defined the default value as “yes“. This targets all countries by default.

We then assigned the value of “no” to the countries we wanted to allow traffic from.

With this defined, we can target countries based on their value within the $block_checkout_country variable by using an if statement.

Learn more about the Map Module here:https://nginx.org/en/docs/http/ngx_http_map_module.html

### How the Location Block Works

Location blocks [contexts] allow us to define and configure how specific URIs are handled by the server. In a sense, by creating a location block for a URI, we’re diverting traffic down a different route than the standard page lookup.

In this example, this allows us to use an if statement to define two different sets of behaviours depending if the request is coming from the US or Canada, or from any other country.

The route we divert traffic down needs to have two different end destinations defined. The first will be a 403 Forbidden error for non-US or Canada countries, and the second is the regular page we want traffic from the US and Canada to arrive at.

Thus our block looks like this:

```
location /checkout/ {
if ( $block_checkout_country = "yes" ) {
return 403;
}
try_files $uri $uri/ /index.php?$args;
}
```

try_files here first checks for and tries to serve the URI. If this doesn’t exist, it passes the request to index.php which in turn passes the request through the PHP location block and, finally, is sent to the PHP-FPM server for processing.

If we didn’t include this in the location block, the server would have nothing to server and it would result in a 404 not found error.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

