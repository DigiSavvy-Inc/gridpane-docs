# How to Configure WebP Express to Serve WebP Images on Nginx | GridPane

# How to Configure WebP Express to Serve WebP Images on Nginx

 

3 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

One of our awesome clients brought the WebP Express plugin to my attention recently, and if you’re looking for an alternative to Shortpixel that simply takes care of the .jpeg/.png conversion to .webp and serves them, this plugin is well worth checking out.

 

## Step 1. Install and Configure the Plugin

Install the plugin on your chosen site, then head to Dashboard > Settings > WebP Express to open the configuration page.

Ignore all the messages about .htaccess. This is only for Apache / LiteSpeed / OpenLiteSpeed. We’ll be setting our rules for Nginx directly on our server in the next steps. The plugin author has streamlining the UI for Nginx on their roadmap for the future.

The plugin offers multiple settings for image quality and different conversion methods. Fine tune them as you see fit. In my testing I left the defaults, and the “cwebp” conversion method worked perfectly well.

 

## Step 2. SSH into your server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 3: Create webp-mappings.conf

We first need to create an Nginx configuration (aka config / .conf) file so that our server can serve WebP files. This first config makes use of the HTTP Context which applies server-wide.

HTTP Context includes the following:

```
http {  include /etc/nginx/common/basics.conf;  #include /etc/nginx/common/geoip.conf;  include /etc/nginx/common/limits.conf;  include /etc/nginx/mime.types;  include /etc/nginx/common/ssl.conf;  include /etc/nginx/common/logging.conf;  include /etc/nginx/common/6g-mappings.conf;  include /etc/nginx/conf.d/*.conf;  include /etc/nginx/extra.d/http-context.conf;  include /etc/nginx/sites-enabled/*;}
```

We’ll make use of the include highlighted in red to create our new config, which ensures that any .conf file added to the /etc/nginx/conf.d/  directory applies server-wide.

This step will only need to be set up once per server. If you’re using WebP Express on more than one site, you can skip this step for your 2nd site onwards.

So, to summarise, we’ll create a file called webp-mappings.conf in the /etc/nginx/conf.d/ directory.

### CREATE WEBP-MAPPINGS.CONF

Create the file with the following command:

```
nano /etc/nginx/conf.d/webp-mappings.conf
```

Paste the following block of code:

```
map $http_accept $webp_suffix {default ""; "~*webp" ".webp"; }
```

Now Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

 

## Step 4: Create webp-main-context.conf

### Create a site-specific configuration

We need to create a file called webp-express-main-context.conf  in /var/www/site.url/nginx.

Create the file with the following, switching out “site.url” with your website’s domain:

```
nano /var/www/site.url/nginx/webp-express-main-context.conf
```

Paste the following block of code:

```
# WebP Express rules
# --------------------
location ~* ^/?wp-content/.*\.(png|jpe?g)$ {
add_header Vary Accept;
expires 365d;
if ($http_accept !~* "webp"){
break;
}
try_files
/wp-content/webp-express/webp-images/doc-root/$uri.webp
$uri.webp
/wp-content/plugins/webp-express/wod/webp-on-demand.php?xsource=x$request_filename&wp-content=wp-content
;
}

# Route requests for non-existing webps to the converter
location ~* ^/?wp-content/.*\.(png|jpe?g)\.webp$ {
try_files
$uri
/wp-content/plugins/webp-express/wod/webp-realizer.php?wp-content=wp-content
;
}
```

Now Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano. You can now proceed to step 5.

 

## Step 5: Check and reload Nginx

Finally, we need to check if the conf files are correct then reload Nginx.

Test your nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

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

