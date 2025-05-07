# How to add your own custom Nginx headers (or reset existing headers) | GridPane

# How to add your own custom Nginx headers (or reset existing headers)

 

5 min read 

To add a custom header to your websites you can use the more_set_headers directive.https://github.com/openresty/headers-more-nginx-module

This article will walk you through how to: –

 

## Adding headers to individual websites

If you want to add the header on a site by site basis, add the following Nginx directive and value in a file on this file path: /var/www/site.url/nginx/*-main-context.conf

This uses the *-main-context.conf. You can replace the * with your own custom name. This is an example how the above code would look if we added a custom header to GridPane and called it “gpheader”:

```
/var/www/gridpane.com/gpheader-main-context.conf
```

Create the file with nano (switching out “site.url” for your domain name):

```
nano /var/www/site.url/nginx/yourchosenname-main-context.conf
```

Add your custom header, for example:

```
more_set_headers {your header code};
```

Hit CTRL+O and then Enter to save the file. CTRL+X to exit nano.

### Check and reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

 

## Add a custom header to all websites on your server

If you’d like to to add this header to all your sites, then you can add it to the extra.d main context configuration located here: /etc/nginx/extra.d/main-context.conf

First, navigate to the following directory:

```
cd /etc/nginx/extra.d/
```

Edit the main-context.conf with:

```
nano main-context.conf
```

Add your custom header, for example:

```
more_set_headers {your header code};
```

Hit CTRL+O and then Enter to save the file. CTRL+X to exit nano.

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

 

## Formatting

The formatting is important when using more_set_headers.

For example, you may have documentation that lists a header as follows:

```
add_header X-Content-Type-Options "nosniff";
```

Using more_set_headers we need to reformat it into exactly what it will look like in the browser’s network tab. In this case, the above would be set as follows:

```
more_set_headers "X-Content-Type-Options: nosniff";
```

What’s contained within the quotation marks is what appear in the browser. You will get Nginx syntax errors if you try and set your header like this:

```
more_set_headers "X-Content-Type-Options "nosniff"";
```

 

## Resetting existing headers

The GridPane stack sets numerous headers and while these are set to a common-sense default, they can be reset and reconfigured for different use cases on an as per your requirements.

To reset a header we need first to clear the existing header, and then afterwards we can set it again as a new header.

This can be accomplished by using the more_clear_headers directive to first clear the header you want to reset, and then use the more_set_headers to set the new header. For example:

```
more_clear_headers "Cache-Control";
more_set_headers "Cache-Control: public, no-transform";
```

This is probably best done on a site by site basis, and we’ll use the *-main-context.conf include to place our code. To get started, create file called cache-control-main-context.conf with the following command, switching out “site.url” with your domain name:

```
nano /var/www/site.url/nginx/cache-control-main-context.conf
```

Enter your code for clearing and reseting your header, and then hit CTRL+O and then Enter to save the file. CTRL+X to exit nano.

### Check and reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

 

## Reset headers on static files

The main context is for handling dynamic files, whereas the headers for static files are handled in the static context. To reset/remove headers from static files you will need to add an additional include in the static context.

### Remove Static File Headers

The process is essentially the same as the section above just with a different config name.

First, create a file called staticfile-headers-static-context.conf with the following command, switching out “site.url” with your domain name:

```
nano /var/www/site.url/nginx/staticfile-headers-static-context.conf
```

Enter your code for clearing and resetting your header, and then hit CTRL+O and then Enter to save the file. CTRL+X to exit nano.

### Check and Reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

 

## Examples of using custom headers for debugging

Custom headers can also be helpful when debugging. The following are a couple of examples of different use cases.

### Example 1. Show Real IP addresses from Cloudflare

The following will show the real IP address of a visitor when you’re using Cloudflare.

Create a site-specific config using the *-main-context.conf include (switching out “site.url” with your domain name):

```
nano /var/www/site.url/nginx/showrealip-main-context.conf
```

Add the following header to the file:

```
more_set_headers "realip-remote-address: $realip_remote_addr";
```

Hit CTRL+O and then Enter to save the file. CTRL+X to exit nano. You’ll then need to check your Nginx syntax and reload Nginx.

### Example 2. Show the stages of key processing for the cache key

The following would show the structure of the cache key as being processed:

```
more_set_headers "key-variables: $scheme$request_method$host$request_uri";
more_set_headers "escaped-key: $escaped_key";
more_set_headers "cache-key: $key";
```

Create a config for the above code block with the following command (switching out “site.url” with your domain name):

```
nano /var/www/site.url/nginx/keys-php-context.conf
```

Paste the code block above, and then hit CTRL+O and then Enter to save the file. CTRL+X to exit nano. Check and reload Nginx as outlined below.

### Check and reload Nginx

Test our Nginx syntax with:

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

