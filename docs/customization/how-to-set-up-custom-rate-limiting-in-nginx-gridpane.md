# How to Set up Custom Rate Limiting in Nginx | GridPane

# How to Set up Custom Rate Limiting in Nginx

 

4 min read 

## Introduction

If find that a site needs additional rate limiting that our defaults don’t cover, this article will demonstrate how to create your own custom rate limiter.

We’ll be specifically looking at rate limiting bots in this article, but the principles remain the same no matter what you’re looking to implement.

### Table of Contents

You can also learn more about Nginx Rate Limiting here:

### Getting Started

The steps in this article require connecting to your server via SSH. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## About the Default GridPane Rate Limits

GridPane limits are configured in this file:

```
/etc/nginx/common/limits.conf
```

Out of the box, there are 2 zones. The one and wp zone:

```
limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;limit_req_zone $rate_limit_input_variable zone=wp:10m rate=6r/s;
```

This does the following:

While we don’t generally recommend, details on how to adjust these settings can be found here:

 

## Creating a Custom Rate Limiter

Creating a custom rate limiter requires directly modifying the limits.conf file.

We strongly recommend that you keep our defaults in place, and you can your own to the bottom of the file.

However, before doing this, copy the original limits.conf to /etc/nginx/extra.d/_common to ensure that changes made are persisted through any update.

 

### Step 1. Edit the limits.conf

First, open the limits.conf in nano with the following:

```
nano /etc/nginx/common/limits.conf
```

The following code block targets the bots and sets the custom variable and you can add it right before the line that reads limit_req_status 503;:

```
##Rate limit crawler bots
map $http_user_agent $isbot_ua {
default 0;
~*(GoogleBot|bingbot|YandexBot|mj12bot) 1;
}
map $isbot_ua $limit_bot {
0 "";
1 $binary_remote_addr;
}
```

Then [configure and] add this to the very bottom of the config:

```
limit_req_zone $limit_bot zone=bots:10m rate=10r/m;
```

The limit_req_zone directive defines the parameters for rate-limiting, and we’ve created a new zone called “bots” which allows us to target the user agents detailed above and limit them to 10 requests per minute. However, we still need to set the limit_req directive at the site level to implement the actual rate limiting.

Modify the above for your use case, then save the file with CTRL+O and then Enter. Exit nano with CTRL+X.

 

### Step 2. Ensure our changes persist

Copy with the following command:

```
cp /etc/nginx/common/limits.conf /etc/nginx/common/_custom/limits.conf
```

 

### Step 3. Add Burst Limits for your site

Now we need to actually limit the request rate. The code is Step 1 above is server wide, we’ll limit the request at the site level. Run the following (switching out site.url for your website URL):

```
nano /var/www/site.url/nginx/limits-root-context.conf
```

The following targets the newly created bot zone and sets the burst limit to 5. This allows a burst of 5 requests within a short time of one another, but still only allows a max of 10 per minute.

Configure for your needs and add to the file:

```
limit_req zone=bots burst=5 nodelay;
```

Save the file with CTRL+O and then Enter. Exit nano with CTRL+X.

 

### Step 4. Check and Reload Nginx

Check the Nginx configuration file with:

```
nginx -t
```

If no errors are returned, reload Nginx with:

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

