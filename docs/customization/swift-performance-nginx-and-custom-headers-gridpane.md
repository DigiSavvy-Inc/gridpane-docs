# Swift Performance, Nginx and Custom Headers | GridPane

# Swift Performance, Nginx and Custom Headers

 

4 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

Swift Performance is a solid caching plugin – right up there at the top of the heap alongside WP Rocket in terms of caching plugin performance.

While neither of these can compete with server-level caching in terms of performance or handling concurrent users, they can still produce excellent results on our stack.

That all said, Swift Performance can actually integrate with Nginx Helper according to their documentation, although this comes at a cost. You can also add their Rewrite Rules directly to an Nginx configuration file.

 

## Swift Performance, Nginx Helper, and Custom Headers

Swift Performance does integrate with Nginx Helper according to their documentation:

“Swift Performance supports Nginx Helper. If you install and configure Nginx Helper properly, Swift will clear Nginx/FastCGI/Redis when cache was cleared in Swift”https://swiftperformance.io/faq/nginx-fastcgi-redis-support/

However, this does come at a cost – you can’t use custom headers. The following information is from a GridPane user who was in contact with their support:

Keeping existing headers is available only with Disk cache + PHP for Nginx. With Disk cache + Rewrites is available only for Apache.

The following paragraph is taken directly from their documentation (source link below):

“Keep Original Headers – If you are using a plugin which send custom headers you can keep them for the cached version as well. Some security plugins add nosniff response header and some other headers-. With this feature you can keep your original headers. This feature is available only in Pro version.”https://swiftperformance.io/documentation/swift-settings-caching-tab/

 

## Using Disk Cache + Rewrites with GridPane

As mentioned above, if you choose to use this option you won’t be able to use custom headers.

If you’re cool with that, then below is how to add Swift’s Rewrite rules to your website via Nginx.

### Step 1. SSH into your server:

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Configure Swift Performance

First, head to Dashboard > Settings > Swift Performance

Then click through to the settings page, click caching in the left hand sidebar, and select Disk Cache with Rewrites from the dropdown. Save the changes.

These may change as you change your settings (e.g. adding a specific page

```
###BEGIN Swift Performance###

set $swift_cache 1;
if ($request_method = POST){
	set $swift_cache 0;
}

if ($args != ''){
	set $swift_cache 0;
}

if ($http_cookie ~* "(wordpress_logged_in)") {
	set $swift_cache 0;
}

if ($request_uri ~ ^/wp-content/cache/swift-performance/([^/]*)/assetproxy) {
      set $swift_cache 0;
}

if (!-f "/var/www/site.url/htdocs/wp-content/cache/swift-performance//$http_host/$request_uri/desktop/unauthenticated/index.html") {
	set $swift_cache 0;
}

if ($swift_cache = 1){
    rewrite .* /wp-content/cache/swift-performance/$http_host/$request_uri/desktop/unauthenticated/index.html last;
}

location ~ desktop/unauthenticated/index.html {
	add_header Link "</wp-content/cache/swift-performance/$http_host$request_uri/css/desktop-full.css>; rel=preload; as=style,</wp-content/cache/swift-performance/$http_host$request_uri/js/desktop-scripts.js>; rel=preload; as=script";
}

###END Swift Performance###
```

### Step 3. Create your config

We’ll be creating a file called “swift-main-context.conf”. Run the following command switching out “site.url” for your website’s domain:

```
nano /var/www/site.url/nginx/swift-main-context.conf
```

Ctrl+O and then hit enter. Then Ctrl+X to exit nano.

### Step 4. Check and restart Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

Your rewrite rules are now active.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

