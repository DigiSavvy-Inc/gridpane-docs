# GridPane Default Cache Exclusions | GridPane

# GridPane Default Cache Exclusions

 

2 min read 

There are a few things that GridPane doesn’t cache by default. Below is a rundown of what these are, along with the specific code that excludes them.

HTTP POST Requests

We exclude POST requests as these contain data that should not be cached.

```
if ($request_method = POST) {
    set $skip_cache 1;
    set $skip_reason "${skip_reason}-POST";
}
```

#### Logged in Sessions & Cookies

If you’re logged into your WordPress website, every page you visit, including the WP dashboard, is excluded from the cache. This includes WooCommerce and Easy Digital Downloads customers when they are logged into their account.

WordPress login and comment author cookies are excluded from the cache.

Cookies for WooCommerce and Easy Digital Download sessions will also be excluded, whether a customer is logged in or not. These are responsible for keeping track of shopping cart activity and are unique to individual visitors.

```
if ($http_cookie ~* "comment_author|wordpress_[a-f0-9]+|wp-postpass|wordpress_no_cache|wordpress_logged_in|[a-z0-9]+_items_in_cart|woocommerce_cart_hash|woocommerce_items_in_cart|wp_woocommerce_session_|edd_items_in_cart") {    set $skip_cache 1;    set $skip_reason "${skip_reason}-http_cookie";}
```

#### Query Strings

Any URL that includes a query string is not cached.

```
if ($query_string != "") {   set $skip_cache 1;   set $skip_reason "${skip_reason}-query_string";}
```

#### URLs

There are specific pages that GridPane excludes from the cache by default. These are: –

It also includes pages that are setup by WooCommerce and Easy Digital Downloads by default:

For example:

These are unique, dynamic pages for each individual website visitor and display information that’s specific to them only.

```
if ($request_uri ~* "(/wp-admin/|/xmlrpc.php|wp-.*.php|index.php|/feed/|.*sitemap.*\.xml/store.*|/cart.*|/my-account.*|/checkout.*|/addons.*)") {    set $skip_cache 1;    set $skip_reason "${skip_reason}-request_uri";}
```

Default User-Defined Skip Cache Include wildcards

You can also create your own skip cache exclusions by adding them to the appropriate Redis or FastCGI .conf located based upon the wildcard includes contained in sites Nginx virtual server:

```
/var/www/site.url/nginx/*-skip-redis-cache-context.conf
/var/www/site.url/nginx/*-skip-fcgi-cache-context.conf
```

So for example if you had a site gridpane.com and it was using Nginx Redis caching, but you needed to exclude the page gridpane.com/awesomesauciness then you would create the following file:

```
/var/www/gridpane.com/nginx/awesome-skip-redis-cache-context.conf
```

Within the file you could add the following skip cache block:

```
if ($request_uri ~* "(/awesomesauciness)") {
    set $skip_cache 1;
    set $skip_reason "${skip_reason}-too_awesome_to_cache";
}
```

You can learn more about excluding pages from your cache here:https://gridpane.com/kb/exclude-a-page-from-server-caching/

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

