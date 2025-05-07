# Nginx Rate Limiting and Plugins (Including Oxygen) | GridPane

# Nginx Rate Limiting and Plugins (Including Oxygen)

 

9 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

## Introduction

This article was originally focused on the Oxygen Builder, which is our most common support request when rate-limiting occurs. It can happen with other plugins too though, and while the example below is from Oxygen, the same steps and advice apply to any plugin that hits rate limiting issues.

Known plugins that may trigger rate limiting include:

*Please read the info box below. 

 

### APRIL 2021 UPDATE

As of April 22nd 2021, Oxygen and Better Search Replace are now whitelisted from our Zone WP rate limiting (detailed below) and no additional configuration is required for either of these plugins. If you have a suggestion for another popular plugin, please let us know.

## Checking the Nginx Error Log

Oxygen tends to hammer the WordPress backend, and sometimes gets tripped up on our rate limiting. Specifically, if you’re trying to sign shortcodes, you may see the following in your Nginx Error Log:

2020/04/25 10:50:52 [error] 30125#30125: *710261 limiting requests, excess: 6.364by zone "wp", client: someiphere, server: gridpanedemo.com, request: "POST /wp-admin/admin-ajax.phpHTTP/1.1", host: "gridpanedemo.com", referrer: "https://gridpanedemo.com/wp-admin/admin.php?page=oxygen_vsb_sign_shortcodes"

The solution is to increase our rate limit. Below is how to do this both for individual websites or server-wide for all your websites on your server. What you choose will depend on your requirements, for example, if you’re using Oxygen on each of your websites, you may wish to implement this server-wide and plan on leaving them high.

We recommend adjusting things for just one specific website and then turn them back down once you’re done.

When checking your Nginx Error Log, you’re looking to determine how many requests per second are taking place so that you can adjust the values below accordingly.

 

## About Zone WP

Zone WP defaults to a 6 request burst queue when the rate limit of 3 requests per second has been exceeded. This zone protects the wp-admin and specifically the admin-ajax endpoint.

Certain plugins (such as Oxygen before we added whitelisting for it – see the infobox above) that hit this endpoint at a rapid rate may need this increase temporarily to handle the rate. We recommend lowering the burst rate again once the process has been completed.

 

## Adjusting Zone WP Rate Limits

Below we’ll look at how to adjust the Zone WP rate limits for specific, individual websites or the entire server.

### Site-Specific Zone WP Rate Adjustment

This is site-specific and allows for a nodelay burst to be set, so if you reach your limit (default is 6) and set the burst to 30, then it would queue up another 30 requests and serve them immediately before dropping requests.

This per-site burst queue is set in addition to the server-wide request per second rate limit (detailed below)

Directive: limit_reqConfig location: /etc/nginx/common/{site.url}-wpcommon.confContext: serverDefault value: 6Accepted values: integer, fqdn

```
gp stack nginx limits -site-zone-wp-burst {queue.size} {site.url}
```

Example:

```
gp stack nginx limits -site-zone-wp-burst 30 gridpane.com
```

### Server-Wide Zone WP Rate Adjustment

With this solution, you are adjusting the total req per second allowed. We set this as standard for 10MB space for keys and 3 requests per second. With each site allowing a burst of 6, that means your sites will serve 9 requests per second before dropping requests.

In addition to this request per second limit, each site has a burst queue (detailed above).

Directive: limit_req_zoneConfig location: /etc/nginx/common/limits.confContext: httpUnit: MB (key store size) and Rate (requests/s)Default value: 10 3Accepted values: integers

```
gp stack nginx limits -req-zone-wp {store.size.mb} {req.per.sec}
```

Example:

```
gp stack nginx limits -req-zone-wp 15 10
```

### Check Nginx for Errors and Reload

Once finished setting either your site adjust or server-side adjustment above, be sure to test the Nginx config for errors and then reload.

Test the configuration with this command:

```
nginx -t
```

If no errors are present, reload the configuration with this command:

```
gp ngx reload
```

 

### Recheck Nginx Error Log and adjust as needed

Once these have been set, try again and if there are any issues recheck your Nginx error log. You may need to further increase.

 

### Reset Limits back to lower threshold when complete

We recommend that you reset your limits back to a lower threshold once you have finished the task at hand. Rate limiting is an important part of server hardening and helps maintain stability across sites.

 

## Zone WP Whitelisting

By default, GridPane whitelists the localhost IP (127.0.0.1) and any URIs that contain the following strings:

The above means that requests made from the server locally, or requests that include the strings in the above list in the URL will not hit our rate limits.

This covers the majority of use cases that we’ve seen. This covers Oxygen shortcode signing, CSS regeneration, and Better Search Replace search and replaces.

The next 2 sections of this article will walk you through the details of how to set up your own whitelisting rules for either request URIs or IP addresses server-wide.

 

## Custom Rate Limit Whitelist Rules for Request URIs

We have the following include which allows you to define and whitelist your own requests and whitelist them server-wide:

```
include /etc/nginx/extra.d/*request-uri-rate-limit-whitelist.conf
```

This include is inside /etc/nginx/common/limits.conf, in the following block:

```
map $request_uri $limited_request_uri {
    default 1;
    include /etc/nginx/extra.d/*request-uri-rate-limit-whitelist.conf;
    ~load-scripts.php 0;
    ~load-styles.php 0;
    ~page=oxygen_vsb_sign_shortcodes 0;
    ~page=oxygen_vsb_settings&tab=cache 0;
    ~page=better-search-replace&bsr-ajax=process_search_replace 0;
}
```

The steps below detail how to create your own whitelist rule/s.

### Step 1. Create the Config

To add whitelist your own URI, you will first need to use the include to create a configuration file:

```
nano /etc/nginx/extra.d/{yourname-}request-uri-rate-limit-whitelist.conf
```

In this example I’m replacing {yourname-} above with “plugin-“, but feel free to name add your own prefix, and create the file as follows:

```
nano /etc/nginx/extra.d/plugin-request-uri-rate-limit-whitelist.conf
```

### Step 2. Add your URI/s

Now add your URI as follows:

```
~my-request-uri.php 0;
```

As you can see above, this line will be inserted into the block along with the default URIs, and the “0” at the end tells Nginx not to apply rate-limiting to this URI.

If you need to whitelist more than 1, simply add each URI on their own line. E.g:

```
~my-request-uri.php 0;
~another-request-uri=ajax 0;
```

### Step 3. Save the Conf

Save the file with CTRL+0 followed by Enter. Exit nano with CTRL+X.

### Step 4. Check and Reload Nginx

Now we need to check the configuration with this command to ensure there are no syntax errors:

```
nginx -t
```

If no errors are present, reload the configuration with this command:

```
gp ngx reload
```

 

## Custom Rate Limit Whitelist Rules with the $http_referer Variable

We have the following include which allows you to define and whitelist your own requests and whitelist them server-wide:

```
include /etc/nginx/extra.d/*referer-rate-limit-whitelist.conf;
```

This include is inside /etc/nginx/common/limits.conf, in the following block:

```
map $http_referer $limited_request_referer {
    default $limited_request;
    include /etc/nginx/extra.d/*referer-rate-limit-whitelist.conf;
    ~page=oxygen_vsb_sign_shortcodes 0;
    ~page=oxygen_vsb_settings&tab=cache 0;
    ~ct_builder=true 0;
    ~page=better-search-replace 0;
}
```

The steps below detail how to create your own whitelist rule/s.

### Step 1. Create the Config

To add whitelist your own http referer, you will first need to use the include to create a configuration file:

```
nano /etc/nginx/extra.d/{yourname-}referer-rate-limit-whitelist.conf
```

In this example I’m replacing {yourname-} above with “plugin-“, but feel free to name add your own prefix, and create the file as follows:

```
nano /etc/nginx/extra.d/plugin-referer-rate-limit-whitelist.conf
```

### Step 2. Add your http referrer/s

Now add your http referrer as follows:

```
~my-referrer=true 0;
```

As you can see above, this line will be inserted into the block along with the default URIs, and the “0” at the end tells Nginx not to apply rate-limiting to this http referrer.

If you need to whitelist more than 1, simply add each on their own line., for example:

```
~my-referrer=true 0;
~another-referrer=something 0;
```

### Step 3. Save the Conf

Save the file with CTRL+0 followed by Enter. Exit nano with CTRL+X.

### Step 4. Check and Reload Nginx

Now we need to check the configuration with this command to ensure there are no syntax errors:

```
nginx -t
```

If no errors are present, reload the configuration with this command:

```
gp ngx reload
```

 

## Custom Rate Limit Whitelist Rules for IP Addresses

We have the following include that allows you to create IP based whitelists to this rate-limiting server-wide:

```
include /etc/nginx/extra.d/*remote-addr-rate-limit-whitelist.conf
```

This include is inside /etc/nginx/common/limits.conf, in the following block:

```
map $remote_addr $is_limited {    default $limited_request_uri;    include /etc/nginx/extra.d/*remote-addr-rate-limit-whitelist.conf;    127.0.0.1 0;}
```

The steps below detail how to whitelist your own IP/s.

### Step 1. Create the Config

To add whitelist your own IP/s you will first need to use the include to create a configuration file:

```
nano /etc/nginx/extra.d/{yourname-}remote-addr-rate-limit-whitelist.conf
```

In this example I’m replacing {yourname-} above with “mynetwork-“, but feel free to name add your own prefix, and create the file as follows:

```
nano /etc/nginx/extra.d/mynetwork-remote-addr-rate-limit-whitelist.conf
```

### Step 2. Add your IP/s

Now add your IP address as follows:

```
199.199.199.199 0;
```

As you can see above, this line will be inserted into the block along with the default localhost IP address “127.0.0.1”, and the “0” at the end tells Nginx not to apply rate-limiting to this IP.

If you need to whitelist more than 1, simply add each IP address on their own line. E.g:

```
199.199.199.199 0;
123.456.789.10 0;
```

### Step 3. Save the Conf

Save the file with CTRL+0 followed by Enter. Exit nano with CTRL+X.

### Step 4. Check and Reload Nginx

Now we need to check the configuration with this command to ensure there are no syntax errors:

```
nginx -t
```

If no errors are present, reload the configuration with this command:

```
gp ngx reload
```

 

 

### Info

The includes above only work for the wp zone which covers interal wp-admin requests, it doesn't whitelist for the wp-login rate limiting.

The whitelist works by making the wp zone input variable $rate_limit_input_variable == 0 so when it is called in a sites /etc/nginx/common/site.domain-wpcommon.conf like so:
location ~ /wp-admin/admin-ajax.php$ {
    ...
    limit_req zone=wp burst=6 nodelay;
    ...
}
Nginx skips the rate limit as no input variable was set.

## Recheck Nginx Error Log

Once your whitelist is in place, retry the request that was rate-limited and check your Nginx error log again. It should proceed without any issues, and there should be no record of it in the log.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

