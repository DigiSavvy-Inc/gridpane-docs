# What is the optimal caching strategy for GridPane, should I run a plugin cache? | GridPane

# What is the optimal caching strategy for GridPane, should I run a plugin cache?

 

3 min read 

We get asked this question a lot, and the answer here is that it varies significantly. Just as no two kids are the same (as most parents with two or more kids would attest), no two sites are the same either :). What works optimally for one site, may not be optimal for another site. That being said, here are some guidelines:

### Should I run a plugin like Swift, WP Rocket, etc?

We almost always recommend our server-level caching options over any kind of plugin caching solution.

Generally speaking, running a plugin like these, the caching part of it won’t move the needle as long as you’re using one of our server-level caches, but the site optimizations like CSS minification, JS deferments, image optimizations, those types of optimizations can definitely move the needle.

However, if you choose to run these plugins, we would recommend either disabling the caching component of these plugins or disabling our server-level cache. If you do run both caches, what tends to happen is that the cache will become cross poisoned. The plugin cache will be cleared, but the server cache will still have some data in it, and it’ll lead to errors on the site, visual errors, etc.

In the GridPane UI, the Redis Page Cache and FastCGI toggles are for Full Page Caching. This is not to be confused with Redis Object Caching which has its tab and toggle.

For Redis and FastCGI Full Page Caching, you need to have Nginx Helper installed and configured. Full documentation of our available Nginx caching options be found here:

### What’s the best caching setup for an eCommerce site?

The ideal setup we would recommend is Redis Full Page Caching and Redis Object Caching.

### What’s the best caching setup for a static brochure site?

We would recommend Redis Page Caching. Redis Object Caching would be optional.

### What’s the best caching setup for a WaaS?

Generally, we recommend Redis Full Page Caching and Redis Object Caching.

However, it can sometimes be easy to use a plugin like WP Rocket, so your clients are able to more intuitively clear their own caches, and you can purge individual subsites much more easily. We’d recommend Redis Object Caching as well, and you should have no issues using plugin-based page caching and server-level object caching.

### What’s the best caching setup for a site that updates/publishes new content regularly?

FastCGI Page Caching and Redis Object Caching will usually work out best for a website like this. FastCGI uses micro-caching and it will keep itself up-to-date in the background as changes are made to the website, and you won’t need to micromanage purging the cache and checking things look as they should.

### An Overview of Your Caching Options

Just as a general overview on potential options, you can do the following combinations:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

