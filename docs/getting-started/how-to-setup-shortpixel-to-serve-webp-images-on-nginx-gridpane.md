# How to Setup ShortPixel to Serve WebP Images on Nginx | GridPane

# How to Setup ShortPixel to Serve WebP Images on Nginx

 

7 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

 

### .AVIF Images

ShortPixel now supports AVIF images. This MIME type is supported by GridPane, and unlike WebP images, no additional server configuration is required for them to work.

### Table of Contents

 

## Introduction

This article will walk you through how to setup Shortpixel to serve webp files on specific websites on your GridPane servers.

CDN Note: Shortpixel state that serving webp images won’t work properly if you use a CDN system (e.g. Cloudflare). Experience from our own users suggests that it will actually work fine as long as Shortpixel is configured properly. Please note that if you are having an issue, always make sure that you disable your CDN or Cloudflare’s proxy before anything else and confirm things are working correctly when these are out of the picture.

See the official Shortpixel documentation here:https://help.shortpixel.com/article/111-configure-nginx-to-transparently-serve-webp-files-when-supported

 

AVIF images

 

## AVIF Configuration

Using AVIF images on Nginx does not require any server side configuration. You can set this up directly within ShortPixels Advanced settings which can be found under Dashboard > Settings > ShortPixel > Advanced:

Toggle on the create AVIF images setting and Deliver images on the frontend setting. Here it will automatically set things via the “Using the <PICTURE> tag syntax” setting. You can leave the preselected “Only via Wordpress hooks (like the_content, the_excerpt, etc)” setting.

Once this is all set, click either the Save changes or Save and go to the Bulk Processing page button at the bottom of the page.

### Note

If you a notice saying that the plugin cannot verify that AVIF is working it is likely incorrect. You can verify the plugin is working by simply opening an image from the frontend of your site in a new tab and checking its file extension.

 

WebP images

 

## WebP Configuration

Unlike AVIF images, WebP do require some server configuration. Please also note that if you clone the site to a new server, you will need to make sure you add also add the following configuration to this server as server level configurations are not copied across.

 

## Step 1. SSH into your server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2: Create webp-mappings.conf

We first need to create an Nginx configuration (aka config / .conf) file so that our server can serve WebP files. This first config makes use of the HTTP Context which applies server-wide.

HTTP Context includes the following:

```
http {
  include /etc/nginx/common/basics.conf;
  #include /etc/nginx/common/geoip.conf;
  include /etc/nginx/common/limits.conf;
  include /etc/nginx/mime.types;
  include /etc/nginx/common/ssl.conf;
  include /etc/nginx/common/logging.conf;
  include /etc/nginx/common/6g-mappings.conf;
  include /etc/nginx/conf.d/*.conf;
  include /etc/nginx/extra.d/http-context.conf;
  include /etc/nginx/sites-enabled/*;
}
```

We’ll make use of the include highlighted in red to create our new config, which ensures that any .conf file added to the /etc/nginx/conf.d/  directory applies server-wide.

This step will only need to be set up once per server. If you’re adding Shortpixel to more than one site, you can skip this step for your 2nd site onwards.

So, to summarise, we’ll create a file called webp-mappings.conf in the /etc/nginx/conf.d/ directory.

### Create webp-mappings.conf

Create the file with the following command:

```
nano /etc/nginx/conf.d/webp-mappings.conf
```

Paste the following block of code:

```
map $http_accept $webp_suffix {
default ""; 
"~*webp" ".webp"; 
}
```

Now Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

 

## Step 3: Create webp-main-context.conf

We now have 2 options for how to proceed. We can apply our WebP settings server-wide, or just on one specific site. You may find that it’s easier and more convenient to simply apply the changes server-wide. We’ll look at both options below.

### Create a Server-wide configuration

The code supplied by Shortpixel themselves only works on individual sites. We’ve modified it so that you can set live for all your sites in one go and then just never need to worry about it.

To set this up, we need to create a file called shortpixel-webp-main-context.conf  in the /etc/nginx/extra.d/ directory.

Create the file with the following command:

```
nano /etc/nginx/extra.d/shortpixel-webp-main-context.conf
```

Paste the following block of code:

```
location ~* ^(/wp-content/.+).(png|jpe?g)$ { 
set $base $1; 
set $webp_uri $base$webp_suffix; 
set $webp_old_uri $base.$2$webp_suffix; 
add_header Vary Accept; 
if ( !-f $document_root$webp_uri ) { 
add_header X_WebP_GP_Miss $document_root$webp_uri; 
} 
try_files $webp_uri $webp_old_uri $uri =404; }
```

Now Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano. You can now proceed to step 4.

### Create a site-specific configuration

For a singular website, we need to create a file called shortpixel-webp-main-context.conf  in /var/www/site.url/nginx.

Create the file with the following, switching out “site.url” with your website’s domain:

```
nano /var/www/site.url/nginx/shortpixel-webp-main-context.conf
```

Paste the following block of code, again switching out “site.url” with your website’s domain:

```
location ~* ^(/wp-content/.+).(png|jpe?g)$ {
set $base $1;
set $webp_uri $base$webp_suffix;
set $webp_old_uri $base.$2$webp_suffix;
set $root "/var/www/site.url/htdocs";
root $root;
add_header Vary Accept;
if ( !-f $root$webp_uri ) {
add_header X_WebP_GP_Miss $root$webp_uri;
}
try_files $webp_uri $webp_old_uri $uri =404;
}
```

Now Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano. Proceed to step 4.

 

 

### Staging Push Note

When pushing from live to staging or vice versa, the site.url in the site-specific config will need to be edited to the correct website (e.g. staging.site.url), otherwise the $root will be incorrect and WebP files will cease to work.

## Step 4: Check and reload Nginx

Finally, we need to check if the conf files are correct then reload Nginx.

Test your nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

 

Additional Notes

 

 

### PHP Notice

If WebP or AVIF images still aren't being served as you expected, please double check your PHP version. If you're still on 7.3, updating to a supported version of PHP is both a good idea and may help resolve this issue for you.

 

### Can't Rerun Images to create WebP's in ShortPixel?

If you can't re-run your images inside Shortpixel to create WebP images, you could accomplish this by installing the WebP Express plugin, running the conversion, and then once you're done you can deactivate and delete it.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

