# Country-Specific Redirects with GeoIP on OpenLiteSpeed (OLS) Servers | GridPane

# Country-Specific Redirects with GeoIP on OpenLiteSpeed (OLS) Servers

 

5 min read 

 

### IMPORTANT

This article is specific to OpenLiteSpeed. For instructions on setting up GeoIP on Nginx, please see this article:
Country-Specific Redirects with GeoIP on Nginx Servers

## Introduction

In this article, we’ll look at how to create redirects for specific countries on OpenLiteSpeed servers. Whether it be for a specific URL, multiple URLs, or to redirect to a country-specific site.

Before we begin, this is just one of many methods available for implementing Geo-specific redirects. There are WordPress plugins available, and Cloudflare also offers this capability. If you need more advanced capabilities, [Geo Targetly](https://geotargetly.com/) may be worth a look. 

## 1. Create a Maxmind Account

This article will walk you through how to use the maxmind geoip2 databases to redirect country level traffic based on the client IP (default) or from a specific variable (supports both IPv4 and IPv6).

The free GeoLite2 databases are available from Maxmind’s website. If you don’t already have one, you can sign up for your account here.

### Activation

The details you need are your Maxmind AccountID + Maxmind License Key.  We now also have stack agnostic commands now that will work on both Nginx and OpenLiteSpeed servers.

To activate this on your server, enter the following command, replacing “{account.id}:{license.key}” with your details:

```
gp stack geoip on {account.id}:{license.key}
```

Example:

```
gp stack geoip on 57679:sd8Hj7kl
```

The Maxmind account information is only required when you first enable GeoIP2. We autogenerate a maxmind config at /etc/GeoIP.conf and store your account details in the server ENV so any subsequent reenabling can use these stored values. The account details allow the maxmind databases to be updated by a weekly cron.

 

## 2. Prepare Your Country Code/s

To implement your redirect you will need the country codes for the specific countries you wish to set things up for.

You can find a list of all available country codes here over on the maxmind website:

ISO 3166 Alpha2 Country Codes

Copy the codes you wish to use.

 

## 3. SSH into Your Server

You will need to SSH into your server to setup your redirects. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## 4. Simple Redirects

Now that we have GeoIP active on the server we can set up our redirect/s. We’re going to place it in the same place we would for regular OLS redirects: /var/www/website.com/ols/rewrites.conf

If you’ve never implemented a redirect on OLS before, this is a simple process, but you may also want to read the following article for further examples of OLS redirects here: How to Create Server Level Redirects on OpenLiteSpeed (OLS).

### Step 1. Create the configuration file

Run the following command, replacing “site.url” with your domain name:

```
nano /var/www/site.url/ols/rewrites.conf
```

### Step 2. Create the redirect

Here’s an example of a simple country redirect for an internal page, for all visitors from France (FR):

```
RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(FR)$RewriteRule ^/?worldwide-url/$ france-only-url/ [L,R]
```

You can setup multiple redirects like so:

```
RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(FR)$RewriteRule ^/?worldwide-url/$ france-only-url/ [L,R]RewriteRule ^/?another-url/$ another-url-fr/ [L,R]RewriteRule ^/?service/$ https://frenchwebsite.fr [L,R]
```

Save the file with CTRL+O and then Enter. Exit with CTRL+X.

### Step 3. Rebuild Your VHConf

As the rewrites.conf file has been modified, a specific OpenLiteSpeed command has to be executed in order for the changes to take effect (replace “site.url” with your domain name):

```
gpols site site.url
```

 

## 5. Multiple Country Redirects

Here we’ll look at how to set up redirects for multiple countries. Here’s an example of how to implement a redirect for multiple countries at the same time:

```
RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(FR|DK|UK)$RewriteRule ^/?worldwide-url/$ countries-url/ [L,R]
```

In the above example, the /worldwide-url will redirect visitors from France, Denmark, and the UK. You can add in the countries you need and setup the redirects you need.

You can also use multiple different redirects like so:

 

```
RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(GB|DK|FR)$
RewriteRule ^/?worldwide-url/$ countries-url/ [L,R]

RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(CA)$
RewriteRule ^/?worldwide-url/$ canada-url/ [L,R]
```

### Step 3. Rebuild Your VHConf

As the rewrites.conf file has been modified, a specific OpenLiteSpeed command has to be executed in order for the changes to take effect (replace “site.url” with your domain name):

```
gpols site site.url
```

 

## 6. Redirect Domain to Separate Country-Specific Domains

### Step 1. Create the configuration file

Create the following file:

```
nano /var/www/site.url/ols/rewrites.conf
```

### Step 2. Set your redirects

Use the following example to create your own redirects:

 

```
RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(FR)$
RewriteRule ^(.*)$ https://domain.fr/$1 [R,L]

RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(DK)$
RewriteRule ^(.*)$ https://domain.dk/$1 [R,L]

RewriteCond %{ENV:GEOIP_COUNTRY_CODE} ^(UK)$
RewriteRule ^(.*)$  https://domain.co.uk/$1 [R,L]
```

Save the file with CTRL+O and then Enter. Exit with CTRL+X.

### Step 3. Rebuild Your VHConf

As the rewrites.conf file has been modified, a specific OpenLiteSpeed command has to be executed in order for the changes to take effect (replace “site.url” with your domain name):

```
gpols site site.url
```

 

## 7. Additional GP-CLI: Update GeoIP, Turn GeoIP On/Off

The following commands can be used to turn GeoIP off and back on:

```
gp stack geoip on gp stack geoip off
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

