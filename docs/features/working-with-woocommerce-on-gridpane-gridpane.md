# Working with WooCommerce on GridPane | GridPane

# Working with WooCommerce on GridPane

 

12 min read 

## Introduction

This article covers multiple topics that are related to working with WooCommerce on GridPane. Not everything covered is applicable to every Woo site. Please refer to each section as necessary.

WooCommerce, regardless of your hosting platform, is often more complex to work with than most other WordPress websites. As we continue to evolve the platform we’ll continue to make WooCommerce easier to work with from a hosting perspective, but for now, this article should cover all the bases.

### Table of Contents

 

## Part 1. Migrating a WooCommerce Store

It pays to plan ahead when migrating a WooCommerce store. You want to make sure that you don’t lose orders or customer data as you move from one server to another, and so there are some steps you should consider in advance. Unlike a regular brochure-style site that can be migrated with zero downtime, you should plan a window where you can put the site in maintenance mode temporarily while you finish up the migration.

The minimum requirements for a successful WooCommerce migration and preventing any lost orders are essentially as follows:

Those simple steps are fine for most stores. However, for bigger, busier websites you may want to consider the steps below.

### Step 1. Plan Ahead

### Step 2. Setup the Website in GridPane

Provision the server, create the website, and provision an SSL.

If your website requires PUT or DELETE requests for the REST API, set these up now in advance (including configuring the 6G / 7G WAF Bad Methods ruleset) – see Part 4 below.

### Step 3. Migrate the Entire Website (Files and Database) and Test

Use your local hosts file to ensure that the website has migrated without any issues. Ensure that everything is working as expected – test that all main functionality is working correctly, and check that the WAF isn’t blocking anything it shouldn’t be.

Also, if you know that nothing new is going to be uploaded to the website, you can migrate all files in advance.

### Step 4. Put the Live Website into Maintenance Mode

To ensure that you don’t miss any orders, put the live website into maintenance mode.

### Step 5. Migrate the Database

Export the database from the live site now that it’s in maintenance mode, and import it into your GridPane site.

### Step 6. Final Checks

### Step 7. Point Your DNS to Your GridPane Server

The migration is complete. Switch your DNS to point to your GridPane server. You can verify that it’s live worldwide here:https://dnschecker.org/#A

 

## Part 2. Server Recommendations & Scaling

Hosting a WooCommerce store comes with some unique challenges, especially as store traffic increases and more sales are made. It’s important to be aware of the different requirements an ecommerce store has vs a regular website.

### Cache Bypassing Traffic

Scaling for cache bypassing traffic and concurrent checkouts is an entirely different hosting problem than scaling for fully cached traffic.

A well-configured server can serve tens of thousands of visitors every minute when serving from the cache, as it’s serving a pre-made page that requires no backend processing to generate it each time.

WooCommerce websites, by necessity, will “BYPASS” the cache when a visitor adds an item to their basket or logs into their account. This is necessary so that visitors do not see someone else’s shopping cart, and so that these details are never cached by the server.

Because of this, PHP and MySQL are required for building every single page from scratch and this requires a lot of CPU power.

### Server Recommendations

This really depends on three main factors:

Concurrent checkouts also become a consideration as the store grows as well, but that goes hand in hand with massive traffic.

We always like to see WooCommerce on their own servers, and any store that makes decent sales or is of a big size should have its own resources (be on its own server).

However, small stores that only make a handful of sales a month really don’t put a whole lot of stress on a server. A few sales per day isn’t going to tax the CPU or impact other sites. You could host a handful of small stores on a 2 CPU 4 GB RAM server, or get away with hosting it on a site with lots of brochure websites.

Move Woo sites to their own server as soon as possible though, and ideally, encourage your clients that it’s the best thing for their business from day one.

### Provider Considerations

At around the $100/month price range, you may want to consider moving to a dedicated server with a high-end CPU. Gaming servers generally come with the DDR4 ECC RAM, and NVMe SSD storage.

Excellent dedicated gaming/high-end CPU server providers include:

### When is it time to Scale Up?

There isn’t an exact formula to follow, but here are some general guidelines:

### Case Study: $650,000 Book Launch

This is a case study on scaling WooCommerce for massive traffic – thousands of concurrent visitors, with 150+ concurrent checkouts. Here you can see how we helped one of our clients host a $650,000 book launch, and how we helped them do it:

How To Provide $5K/month WooCommerce Hosting

 

## Part 3. Caching and PHP Settings Recommendations

We always recommend Object caching for database-intensive websites, especially WooCommerce. We also generally recommend Redis Page Caching for WooCommerce sites well (instead of FastCGI).

If the server is dedicated to this one website then we recommend that you set your PHP worker setting to Static. You can learn more about PHP workers here:

PHP Workers and WordPress: A Guide for Better Performance

 

## Part 4. The Rest API and Fixing 403 / 405 Errors

Two potential errors you may come up against are 403 and 405 errors. These can be caused by a Web Application Firewall (WAF) blocking a request, and/or when a request method such as PUT has not been configured on the server (more below).

403 Forbidden Error: This error code indicates that the server understood the request but refuses to authorize it.

NOTE: For product download 403 errors please see part 5 below.

405 Method Not Allowed: This response status code indicates that the request method is known by the server but is not supported by the target resource.

### HTTP Verbs

For security reasons, modern servers do not allow for PUT or DELETE requests to be available by default.

On Nginx, these aren’t even possible actions within the core HTTP module. To allow PUT and DELETE requests on Nginx, you need to compile in an extra module and make changes for each site.

The lead developers of WordPress are aware that most servers don’t allow these methods, and so they have built an override method into the REST API to take this into account. However, not everyone follows best practices so in some cases you may need to enable these on your servers. This knowledge base article will walk you through the process:

PUT Requests for the WooCommerce API and Other Plugins

### 6G and 7G WAFs

If you use the 6G or 7G WAF you’ll also need to create an exclusion for “bad-methods” or turn the ruleset off. This ruleset specifically blocks: CONNECT DEBUG DELETE MOVE PATCH PUT TRACE TRACK.

 

## Part 5. Product Downloads and WAFs

Downloadable products in WooCommerce will work with both the Force Downloads option and the X-Accel-Redirect/X-Sendfile option. These will also both work out of the box with the 6G WAF and ModSec WAF.

However, when using the 7G WAF a couple of different issues can occur. The fix is quick and easy though, and below is how to configure things.

### Step. 1 Choose “Force Downloads”

Inside WooCommerce choose the Force Downloads option is what you’ll want to use to ensure you don’t hit this error:

“This site can’t be reached ERR_INVALID_RESPONSE“

You can set this inside WooCommerce / Settings / Products / Downloadable Products:

### Step 2. Add an Exclusion Rule

SSH into your server and run the following command (switching our site.url with your websites URL):

```
nano /var/www/site.url/nginx/woo-whitelist-7g-context.conf
```

This will create and open up a new Nginx config in the nano editor. Paste the following code:

```
set $exclusion_rule_match "";if ( $args ~* ^(.*)&order=wc_order_(.*)$ ) {set $exclusion_rule_match 35;}if ( $bad_querystring_7g = $exclusion_rule_match ) {set $7g_drop_bad_query_string 0;}
```

This creates an exclusion for the rule that’s blocking the download with a 403 error.

Save this with CTRL+O followed by Enter. Exit the nano editor with CTRL+X.

### Step 3. Check and Reload Nginx

To set your rule into effect you will need to check your Nginx syntax with:

```
nginx -t
```

If no errors are present, reload Nginx with:

```
gp ngx reload
```

Your rule is now active and product downloads will work correctly.

 

## Part 6. Products Import

If you have a firewall enabled (like 7G), it may block the products from getting imported (from a csv file) with a 403 Forbidden error.

Sample URL of the 403 Forbidden page:

```
https://example.com/wp-admin/edit.php?post_type=product&page=product_importer&wc_onboarding_active_task=product-import&step=mapping&file=/var/www/example.com/htdocs/wp-content/uploads/2021/11/sample_products.csv&delimiter=,&_wpnonce=ed1ecef18b
```

When this happens open your site customizer in your GridPane account, go to 6G WAF/7G WAF under the Security tab, and open the Log file.

Look for a line like this:

```
[30/Nov/2021:22:55:19 +0100] [":bad_request_25:"] xx.xxx.xx.xxx example.com "GET /wp-admin/edit.php?post_type=product&page=product_importer&wc_onboarding_active_task=product-import&step=mapping&file=/var/www/example.com/htdocs/wp-content/uploads/2021/11/sample_products.csv&delimiter=,&_wpnonce=ed1ecef18b HTTP/2.0" 403 0.000 "https://example.com/wp-admin/edit.php?post_type=product&page=product_importer&wc_onboarding_active_task=product-import" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:95.0) Gecko/20100101 Firefox/95.0"
```

What you are particularly looking for in the above is the number in bad_request_25, 25 in this example.

Create a rule to exclude the above.

Connect to your server using SSH via Terminal and run:

```
nano /var/www/example.com/nginx/woo-whitelist-7g-context.conf
```

while replacing example.com with your site’s domain.

Paste the following:

```
set $exclusion_rule_match "";if ( $args ~* ^post_type=product&page=product_importer ) { set $exclusion_rule_match 25;}if ($bad_request_7g = $exclusion_rule_match) { set $7g_drop_bad_request 0;}
```

In the above replace 25 with the bad request number.

To set your rule into effect you will need to check your Nginx syntax with:

```
nginx -t
```

If no errors are present, reload Nginx with:

```
gp ngx reload
```

Your rule is now active and product importing will work correctly. Just reload the 403 page if you still have it open.

 

## Part 7. Staging/Failover Challenges

One of the challenges when using the Staging and Failover features with WooCommerce is making sure customer data and orders don’t go missing.

Snapshot Failover isn’t suitable for most WooCommerce stores as even with a 1 hour sync time the potential for losing customer data is too great.

GridPane offers advanced staging features that allow you to push only files, and select certain database tables means that you can still do some work with a WooCommerce store.

However, WooCommerce stores orders as a custom post type so they’re stored in the wp_posts table. This means you can’t easily exclude WooCommerce orders when pushing from Staging to Live.

Unfortunately, there isn’t a good solution for this. You could use a plugin (or multiple plugins), and put the live site into maintenance mode, export and then import the orders into Staging, then push to Live. You could also use a plugin like WP Migrate DB Pro to sync database changes between Staging and Live.

We don’t have any specific recommendations at this time.  In the future, hopefully, either WooCommerce or an independent plugin will solve the issue by moving everything into custom tables. It’s a little crazy that this hasn’t been done already.

 

## Part 8. Woo + WaaS = Bad Idea

 

 

## Help Us Improve This Article!

Do you have further information that the GridPane community may benefit from when working with WooCommerce? Please let us know by creating a support ticket with your suggestions.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

