# Cookie-free domains and GTMetrix Scores | GridPane

# Cookie-free domains and GTMetrix Scores

 

2 min readHitting a 100/100 score on GTMetrix is certainly possible with WordPress, but the most unintuitive part is usually the “cookie-free domains” metric – also sometimes called “cookieless domains”.

This is actually quite easily fixed by using a CDN such KeyCDN, BunnyCDN or Stackpath. Unfortunately Cloudflare does not offer the ability to disable cookies on their free tier.

Using a CDN is the route we strongly recommend.

Caching, utilizing a CDN, CSS/JS minification and cookie-free domains are the four reasons why a new WordPress installation won’t hit 100/100 out of the box (in most cases).

### Will this actually improve your websites performance?

Highly unlikely, especially not in real world terms. This warning is outdated, and with HTTP/2 and the size of cookies themselves, the method outlined below may actually make your site slower – although this again will likely have minuscule to zero impact.

## The Non-CDN Route

This is all non-standard WP configuration and we recommend testing this first before running it on your live, production website.

### Step 1. Create a redirect subdomain

Inside your GridPane account, click on your website to open up the configuration modal and click through to the domains tab.

Here, click the green button to create an add-on domain, and set it as a 301 redirect. To keep it simple, we recommend using “static” as your subdomain.

### Step 2. Provision an SSL certificate for your redirect subdomain

NOTE: If you’re routing to www on your primary domain, you must also setup the www DNS record for your redirect domain before you provision your SSL certificate.

Once the DNS records are in place, toggle on SSL for your redirect inside the domains tab.

### Step 3. Point your subdomain to /wp-content via wp-config.php

You can edit your wp-config.php downloading, editing and re-uploading it via SFTP, or you can edit directly on your server with nano.

To edit with nano, first SSH in, and then run the following command (switching out “site.url” for your domain):

```
nano /var/www/site.url/wp-config.php
```

Add the following just above the line which reads: /* That's all, stop editing! Happy publishing. */, again switching out “site.url” for your domain:

```
define("WP_CONTENT_URL", "https://static.site.url"); 
define("[COOKIE_DOMAIN](https://codex.wordpress.org/Editing_wp-config.php#Set_Cookie_Domain)", "site.url");
```

To save the file, hit CTRL+O followed by enter. To exit nano hit CTRL+X.

You’re now all set. Head over to GTMetrix and retry.

### Step 4. Celebrate

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

