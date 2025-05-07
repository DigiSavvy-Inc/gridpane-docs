# How to Create Server Level Redirects on OpenLiteSpeed (OLS) | GridPane

# How to Create Server Level Redirects on OpenLiteSpeed (OLS)

 

4 min read 

## Introduction

Sometimes you might need to do different kinds of redirects that aren’t quite covered by our full domain 301 redirects. In this article, we’ll look at how to add server-level redirects to your OpenLiteSpeed (OLS) servers.

### Adding Your Rewrites

When adding your rewrites, we recommend that you use the rewrites.conf instead of your .htaccess file. You’ll find the rewrites.conf inside your sites /ols directory here:

```
/var/www/site.url/ols/rewrites.conf
```

 

## Redirect Formatting

When editing the rewrites.conf, you can add 1 rewrite per line, and the RewriteEngine On is not required.

A simple rewrite rule looks as follows:

```
RewriteRule ^/?old-page$ new-page [L,R=301]
```

We’ll dig a little deeper into this in the examples section below, but above is the basic formatting most 301 redirects follow.

### Migrating from Apache

If you’re migrating redirects from a .htaccess file on Apache you’ll need to make a minor modification to each rewrite for them to work correctly on your OLS servers. Here’s an example of an Apache rewrite:

```
RewriteRule ^myoldpage/(.*)$ mynewpage/$1 [L,R=301]
```

On OLS this would be:

```
RewriteRule ^/?myoldpage/(.*)$ mynewpage/$1 [L,R=301]
```

As you can see here, on OLS you’ll need to add an additional /? before the URI you’re looking to redirect.

For more details on migrating rewrites from Apache to OpenLiteSpeed, check out this article: https://openlitespeed.org/kb/migrate-apache-rewrite-rules-to-openlitespeed/

 

## OLS Redirect Examples

Detailed below are examples of 301 redirects that should cover any use cases you may have.

### 1. Regular Page to Page Redirects

Here’s an example of directing one page on a site to another on the same site:

```
RewriteRule ^/?old-page$ new-page/sub-page [L,R=301]
```

### 2. Wildcard Page Redirects

If you want to move a page and all its subpages you can use the following two rules. The first redirects the old parent page to the new parent page, and the second uses a wildcard to redirect all child pages.

```
RewriteRule ^/?old-page$ new-page/ [L,R=301]
RewriteRule ^/?old-page/(.*)$ new-page/$1 [L,R=301]
```

### 3. Old Domain to New Domain

As this is working with the domain itself, we also need to add a rewrite condition before the RewriteRule.

Here we have the $1 all the subpages of the old domain will map to the equivalent subpage of the new domain. For example, olddomain.com/abc will redirect to newdomain.com/abc. Remove the $1 if you want everything to redirect to the site’s homepage.

```
RewriteCond %{HTTP_HOST} ^olddomain\.com [NC]
RewriteRule ^(.*)$ https://newdomain.com/$1 [L,R=301,NC]
```

Using [NC] flag here ensures the RewriteRule will be case-insensitive.

### 4. Redirecting olddomain.com to newdomain.com/something

Here without the $1 at the end of the new domain URI, all pages of the old domain will redirect to this specific page.

```
RewriteCond %{HTTP_HOST} ^olddomain\.com [NC]
RewriteRule ^(.*)$ https://newdomain.com/something [L,R=301,NC]
```

### 5. Redirecting olddomain.com/something to newdomain.com/somethingelse

```
RewriteRule ^/?something$ https://newdomain.com/something [L,R=301]
```

### Multiple Redirects

To add multiple redirects, add each on their own line. For example:

```
RewriteRule ^/?old-page$ new-page/sub-page [L,R=301]
RewriteRule ^/?other-page$ other-new-page [L,R=301]
RewriteRule ^/?something$ https://newdomain.com/something [L,R=301]
```

 

## Add Your Server Level Redirects

### Step 1. Connect to Your Server

To set up server-level redirects on OLS you will first need to SSH into your server. To get started, please see the following articles:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Edit Your rewrites.conf

To edit the config file, use the following command (switching out site.url with your site URL):

```
nano /var/www/site.url/ols/rewrites.conf
```

Add your rewrites (each on their own line), and then save the file with CTRL+O and then Enter, and exit nano with CTRL+X.

### STEP 3. REBUILD YOUR VHCONF

As the rewrites.conf file has been modified, a specific OpenLiteSpeed command has to be executed in order for the changes to take effect (replace “site.url” with your domain name):

```
gpols site site.url
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

