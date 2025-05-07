# Remove Query Strings from Requests to Load the Cached Version of a Page | GridPane

# Remove Query Strings from Requests to Load the Cached Version of a Page

 

3 min read 

By default, GridPane excludes query strings from the cache, so anytime a visitor loads your website with a query string attached (e.g. yourwebsite.com?123), they load the page from scratch, bypassing the cache, and therefore receive a slower load time on average.

In most cases, this is a good thing, as query strings are unique and it would make no sense to cache them.

For things like Google Analytics and Facebook link referrals, however, you can set up a rule that will rewrite these specific, unique parameters and return the cached version of your page for improved performance.

Below will walk you through how to do this for individual websites or for all the websites on a server.

 

 

### Important

Removing query parameters may (and likely will) interfere with your website analytics and other third-party tracking methods. It is therefore not advisable if your marketing/advertising relies on such analytics. Instead, you may want to consider using Rocket Nginx or OpenLiteSpeed for your website, which you can configure to exclude those parameters directly inside their plugin settings instead of removing them.

### Getting Started

The code block we’ll be adding is as follows:

```
#remove query string/sif ($args ~* "(utm_|gclid|fbclid)") { #? in uri? drops the utm query string rewrite ^(.*)$ $uri? permanent;}
```

The part in bold are the strings we wish to rewrite, and will ensure that any query string beginning with either utm_ (Google Analytics), gclid (Google Adwords), or fbclid (Facebook links) return a cached version of your page. You can modify as per your requirements, and you can add more by separating each with a ” | “.

Example:

```
if ($args ~* "(utm_|gclid|fbclid|qsone|qstwo|qsthree)") {
```

## Remove specific Query Strings from individual websites

If you want to add query string rewrite rules on a site by site basis we can do so here: /var/www/site.url/nginx/*-main-context.conf

This uses the *-main-context.conf. You can replace the * with your own custom name. This is an example of how the above code would look if we added a custom rule to GridPane and called it “qs”:

```
/var/www/gridpane.com/qs-main-context.conf
```

Create the file with nano (switching out “site.url” for your domain name):

```
nano /var/www/site.url/nginx/yourchosenname-main-context.conf
```

Add your rewrite code, for example:

```
#remove query string/sif ($args ~* "(utm_|gclid|fbclid)") { #? in uri? drops the utm query string rewrite ^(.*)$ $uri? permanent;}
```

Hit CTRL+O and then enter to save the file. CTRL+X to exit nano.

### Check and reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

## Remove specific Query Strings from all websites on your server

If you’d like to to add remove specific query strings from all your sites, then you can add this code to the extra.d main context configuration located here: /etc/nginx/extra.d/main-context.conf

First, navigate to the following directory:

```
cd /etc/nginx/extra.d/
```

Edit the main-context.conf with:

```
nano main-context.conf
```

Add your rewrite rule/s, for example:

```
#remove query string/sif ($args ~* "(utm_|gclid|fbclid)") { #? in uri? drops the utm query string rewrite ^(.*)$ $uri? permanent;}
```

Hit CTRL+O and then enter to save the file. CTRL+X to exit nano.

We’ll now copy the file into the _custom directory to ensure the changes persist:

```
cp main-context.conf _custom/main-context.conf
```

Or, alternatively, you can copy the file with:

```
cp /etc/nginx/extra.d/main-context.conf /etc/nginx/extra.d/_custom/main-context.conf
```

### Check and reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

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

