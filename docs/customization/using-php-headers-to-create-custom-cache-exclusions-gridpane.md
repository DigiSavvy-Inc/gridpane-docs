# Using PHP Headers to Create Custom Cache Exclusions | GridPane

# Using PHP Headers to Create Custom Cache Exclusions

 

2 min read 

## Introduction

To offer more flexibility in the way you handle cache exclusions, you can also add a custom PHP header inside of WordPress to exclude pages as you see fit.

### Table of Contents

 

## Nginx Caching Configurations

This will work for both FastCGI and Redis Page caching on GridPane servers.

Out of the box, both of our caching Nginx configurations contain the following:

### FastCGI

```
fastcgi_cache_bypass $skip_cache$upstream_http_do_not_cache;
fastcgi_no_cache $skip_cache$upstream_http_do_not_cache;
```

### Redis

```
srcache_fetch_skip $skip_cache$upstream_http_do_not_cache;
srcache_store_skip $skip_cache$upstream_http_do_not_cache;
```

### What These Do

The above will ensure that if a page has the following HTTP response header, it will result in a cache MISS:

```
do-not-cache: true
```

 

## Add a HTTP Response Header via PHP in WordPress

Setting the header via PHP looks as follows:

 

```

```

### Using the send_headers hook

In WordPress, you can use the send_headers hook to add your headers.

For example, adding this to your themes functions.php would create an exclusion across your entire site:

```
function my_headers() {
header( 'do-not-cache: true' );
}
add_action( 'send_headers', 'my_headers' );
```

You can use the above to create add the do-not-cache header across your site as you see fit, such as adding this to custom page templates and so forth.

 

### Excluding Specific Pages or Categories from functions.php

If you’d like to target specific pages, the send_headers hook detailed above will not work for this use case.

This is because that hook is fired before the main query is initiated correctly. The main query needs to be properly initiated before we can make use of such functions as is_single(<>) to target a specific page or is_category("x") to target a specific category.

The template_redirect is more suitable for this. Your code could look like this:

```
function my_headers() {
if( is_single(your-page-ID-here) ) {
header( 'do-not-cache: true' );
}
}add_action( 'template_redirect', 'my_headers' );
```

Reference: https://wordpress.stackexchange.com/questions/258896/how-can-i-change-http-headers-only-to-posts-of-a-specific-category-from-a-plugin

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

