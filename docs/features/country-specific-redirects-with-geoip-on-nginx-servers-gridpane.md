# Country-Specific Redirects with GeoIP on Nginx Servers | GridPane

# Country-Specific Redirects with GeoIP on Nginx Servers

 

6 min read 

 

### IMPORTANT

This article is specific to Nginx. For instructions on setting up GeoIP on OpenLiteSpeed, please see this article:
Country-Specific Redirects with GeoIP on OpenLiteSpeed (OLS) Servers

## Introduction

In this article, we’ll look at how to create redirects for specific countries. Whether it be for a specific URL, multiple URLs, or to redirect to a country-specific site.

Before we begin, this is just one of many methods available for implementing Geo-specific redirects. There are WordPress plugins available, and Cloudflare also offers this capability. If you need more advanced capabilities, [Geo Targetly](https://geotargetly.com/) may be worth a look. 

## 1. Create a Maxmind Account

The ngx_http_geoip2_module that we will be using creates variables with values from the maxmind geoip2 databases based on the client IP (default) or from a specific variable (supports both IPv4 and IPv6). Using this module you can easily filter traffic by a clients GeoIP based on country or city. Find out more here.

The GeoIp2 module makes use of the free GeoLite2 databases that are available from Maxminds website. If you don’t already have one, you can sign up for your account here.

### Activation

The details you need are your Maxmind AccountID + Maxmind License Key.

To activate this on your server, enter the following command, replacing “{account.id}:{license.key}” with your details:

```
gp stack geoip on {account.id}:{license.key}
```

Example:

```
gp stack geoip on 57679:sd8Hj7kl
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

 

## 4. Simple Redirects

Now that we have GeoIP active on the server we can set up our redirect/s. We’re going to place it in the same place we would for regular Nginx redirects: /var/www/website.com/nginx/*-main-context.conf

If you’ve never implemented an Nginx redirect before, this is a simple process, but you may also want to read the following article for further examples of Nginx redirects here: Nginx Redirects Examples.

### Step 1. Create the configuration file

Run the following command, replacing “site.url” with your domain name:

```
nano /var/www/site.url/nginx/geo-redirect-main-context.conf
```

### Step 2. Create the redirect

Here’s an example of a simple country redirect for an internal page, for all visitors from France (FR):

```
if ( $geoip2_data_country_code = "FR" ) { 
  rewrite ^/worldwide-url/$ /france-only-url permanent; 
}
```

The if statement specifies to only redirect for visitors who are from France, and then we have a regular Nginx redirect.

You can setup multiple redirects like so:

```
if ( $geoip2_data_country_code = "FR" ) {
  rewrite ^/worldwide-url/$ /france-only-url permanent; 
  rewrite ^/another-url/$ /another-url-fr permanent; 
  rewrite ^/service/$ https://frenchwebsite.fr permanent; 
}
```

Save the file with CTRL+O and then Enter. Exit with CTRL+X.

### Step 3. Reload Nginx

Now we need to check our config is correct then reload Nginx.

Test your Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

 

## 5. Multiple Country Redirects

Here we’ll look at two different ways to setup redirects for multiple countries. The first one is the simplest method.

### Method 1

This is an extension of the previous section above, using the same steps, and looks like this:

```
if ( $geoip2_data_country_code ~* "(FR|DK|UK)" ) {    rewrite ^/worldwide-url/$ /countries-url permanent; }
```

In the above example, the /worldwide-url will redirect visitors from France, Denmark, and the UK. You can add in the countries you need and setup the redirects you need.

You can also use multiple if statements for different redirects like so:

 

```
if ( $geoip2_data_country_code ~* "(FR|DK|UK)" ) {
   rewrite ^/worldwide-url/$ /countries-url permanent;
}

if ( $geoip2_data_country_code = "CA" ) {
   rewrite ^/worldwide-url/$ /canada-url permanent;
}
```

Save the file with CTRL+O and then Enter. Exit with CTRL+X.

Check and reload Nginx:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

### Method 2

Here we’ll create a configuration called geo-mappings.conf inside /etc/nginx/conf.d:

```
nano /etc/nginx/conf.d/geo-mappings.conf
```

We can then map our countries like so:

```
map $geoip2_data_country_code $redirect_country {
   default no;
   FR yes;
   DK yes;
   UK yes;
}
```

Save the file with CTRL+O and then Enter. Exit with CTRL+X.

We can then use the same /var/www/site.url/nginx/geo-redirect-main-context.conf like the previous examples.

Create the file with:

```
/var/www/site.url/nginx/geo-redirect-main-context.conf
```

Using what we’ve just created we set redirects like so:

```
if ( $redirect_country = "yes" ) { 
   rewrite ^/worldwide-url/$ /countries-url permanent; 
}
```

Save the file, check and reload Nginx.

 

## 6. Redirect Domain to Separate Country-Specific Domains

If you want to redirect the entire domain to a country-specific domain, instead of using our *-main-context.conf include, we can use our *-root-context.conf include.

### Step 1. Create the configuration file

Create the following file:

```
nano /var/www/site.url/nginx/geo-redirect-root-context.conf
```

### Step 2. Set your redirects

Use the following example to create your own redirects:

 

```
if ( $geoip2_data_country_code = "FR" ) {
   return 301 https://domain.fr$request_uri;
}

if ( $geoip2_data_country_code = "DK" ) {
   return 301 https://domain.dk$request_uri;
}

if ( $geoip2_data_country_code = "UK" ) {
   return 301 https://domain.co.uk$request_uri;
}
```

Save the file with CTRL+O and then Enter. Exit with CTRL+X.

### Step 3. Reload Nginx

Now we need to check our config is correct then reload Nginx.

Test your Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

 

## 7. Additional GP-CLI: Update GeoIP, Turn GeoIP On/Off

The following commands can be used to turn GeoIP off and back on:

```
gp stack geoip on gp stack geoip off
```

On Nginx you can also disable the module entirely:

```
gp stack nginx geoip -disable-module
```

You can update GeoIP with this command:

```
gp stack geoip update
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

