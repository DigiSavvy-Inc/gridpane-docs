# How to Fix the “Error establishing a Redis connection” Error | GridPane

# How to Fix the “Error establishing a Redis connection” Error

 

2 min read 

## Introduction

If you’re seeing “Error establishing a Redis connection” error notices on your WordPress website, this article will explain the available routes to help you resolve the issue.

At the time of writing (August 2023), the following two issues may be causing this on your website:

Servers that are hosting websites that make heavy use of Redis Store (having at least 200 thousand key-value pairs) are more likely to see this issue.

 

## Fix 1. Increase Redis Timeouts

You can increase the Redis timeouts by adding the following to your websites user-configs.php file:

```
// reasonable connection and read+write timeouts
define( 'WP_REDIS_TIMEOUT', 2 );
define( 'WP_REDIS_READ_TIMEOUT', 2 );
```

Adjust the timeout as necessary.

You can learn more about the user-configs.php file here:

Working with the wp-config.php on GridPane and an introduction to user-configs.php

And more about the above code snippet here:

https://github.com/rhubarbgroup/redis-cache/blob/develop/INSTALL.md#3-configuring-the-plugin

 

## Fix 2. Upgrade to Ubuntu 22.04 (Vultr Only Right Now)

### Ubuntu 18.04 Stack

If your website is currently on our Ubuntu 18.04 stack, upgrading to the 22.04 should resolve your issue. You can learn more about the Ubuntu 22.04 stack and migrating your sites here:

The Ubuntu 22.04 Stack Feature Updates

### Ubuntu 20.04 Stack

Due to the changes in WordPress 6.3, we’ve updated our Ubuntu 20.04 stack to move each site to using their own Redis database like our Ubuntu 22.04 stack.

For existing sites, you can take advantage of this update and move them to use their own Redis databases by toggling object caching OFF and then back ON again.

Please note that this will clear the redis cache entirely for that sites keys, so you may want to time this action for a low-traffic hour.

Also, this change will not set any timeouts like detailed in the previous section, which may still be necessary for resource-intensive websites.

 

## If Neither Fix Works

If the above 2 fixes don’t resolve your issue, this will be a resource-driven problem. Allocating more RAM to Redis (instructions can be found here: Configure Redis) and/or upgrading your server so that it has more available RAM may be necessary.

You can also investigate your current codebase and remove resource-hungry plugins, and/pr look at configuring the object cache plugins settings by following their official documentation.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

