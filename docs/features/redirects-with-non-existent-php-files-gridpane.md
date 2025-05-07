# Redirects with non-existent PHP files | GridPane

# Redirects with non-existent PHP files

 

7 min read 

There may be times when you need to move a website that was previously built with URLs that ended in “.php“. For example: www.website.com/about.php.

To ensure that you don’t lose any of the SEO benefits for these pages, you’ll need to set up 301 redirects for them to point to their new URL.

If you’d like to do this using a WordPress plugin, you’ll need to edit a configuration file. This article will walk you through how to do this.

## Step 1. SSH into your server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Identify the Appropriate Nginx Configuration File

The file you’ll need to edit is located inside /etc/nginx/common, and the file you’ll be editing is site.url-{cachetype}.conf.

One of the following three files below will exist depending on the type of caching your website is using.

### Redis Page Caching

If you’re using Redis page caching, you will need to edit the redis configuration file.

File name: site.url-wp-redis.confExample: gridpane.com-wp-redis.conf

### FastCGI Page Caching

If you’re using FastCGI page caching, you will need to edit the FastCGI configuration file.

File name: site.url-wpfc.confExample: gridpane.com-wpfc.conf

### PHP – No Caching

If you have no server page caching toggled on, IE Redis and FastCGI are both off, and instead a regular plugin such as WP Rocket or Swift Performance, you’ll need to edit the PHP configuration file.

File name: site.url-php.confExample: gridpane.com-php.conf

 

## Step 3. Edit the Appropriate Nginx Configuration File

Now that you know the file name you’re looking to edit, below will walk you through the changes necessary for each different option. Please be sure to select the correct option for the caching type your using.

 

 

### Important

If you change your caching type, this remove the file you edit in the steps below, and you will lose your changes. This means your redirects will no longer work. To get them working again, you will need to repeat the process outlined below for your new caching type.

### Redis: Edit the site.url-wp-redis.conf

Open the file in the nano editor with the following command, switching out “site.url” for your websites domain name:

```
nano /etc/nginx/common/site.url-wp-redis.conf
```

For example:

```
nano /etc/nginx/common/yourwebsite.com-wp-redis.conf
```

You can now make your edits. Use your down arrow key to navigate to the bottom of the file. You will see the following block of code, and the line we need to edit is red:

```
location ~ \.php$ {
  #set $key "nginx-cache:$scheme$request_method$host$request_uri$geoip2_data_country_code";
  set $key "nginx-cache:$scheme$request_method$host$request_uri";
  try_files $uri =404;
  srcache_fetch_skip $skip_cache;
  srcache_store_skip $skip_cache;
  srcache_response_cache_control off;
  set_escape_uri $escaped_key $key;
  srcache_fetch GET /redis-fetch $key;
  srcache_store PUT /redis-store key=$escaped_key;
  more_set_headers 'X-Grid-SRCache-TTL $cache_ttl';
  more_set_headers 'X-Grid-SRCache-Skip $skip_reason';
  more_set_headers 'X-Grid-SRCache-Fetch $srcache_fetch_status';
  more_set_headers 'X-Grid-SRCache-Store $srcache_store_status';
  fastcgi_split_path_info ^(.+\.php)(.*)$;
  include /etc/nginx/fastcgi_params;
  include /etc/nginx/extra.d/php-context.conf;
  include /var/www/site.url/nginx/*-php-context.conf;
  #fastcgi_param HTTPS on;
  fastcgi_pass unix:/var/run/php/php73-fpm-ngx.com.sock;
  #http2_push_preload on;
}
```

Here we need to remove the $= 404 from the try_files directive and replace it with $uri/ /index.php?$args, like so:

```
location ~ \.php$ {
  #set $key "nginx-cache:$scheme$request_method$host$request_uri$geoip2_data_country_code";
  set $key "nginx-cache:$scheme$request_method$host$request_uri";
  try_files $uri $uri/ /index.php?$args;
  srcache_fetch_skip $skip_cache;
  srcache_store_skip $skip_cache;
  srcache_response_cache_control off;
  set_escape_uri $escaped_key $key;
  srcache_fetch GET /redis-fetch $key;
  srcache_store PUT /redis-store key=$escaped_key;
  more_set_headers 'X-Grid-SRCache-TTL $cache_ttl';
  more_set_headers 'X-Grid-SRCache-Skip $skip_reason';
  more_set_headers 'X-Grid-SRCache-Fetch $srcache_fetch_status';
  more_set_headers 'X-Grid-SRCache-Store $srcache_store_status';
  fastcgi_split_path_info ^(.+\.php)(.*)$;
  include /etc/nginx/fastcgi_params;
  include /etc/nginx/extra.d/php-context.conf;
  include /var/www/site.url/nginx/*-php-context.conf;
  #fastcgi_param HTTPS on;
  fastcgi_pass unix:/var/run/php/php73-fpm-ngx.com.sock;
  #http2_push_preload on;
}
```

Save the file with CTRL+O, and then Enter. Exit nano with CTRL+X.

You can now move on to step 4.

 

### FastCGI: Edit the site.url-wpfc.conf

Open the file in the nano editor with the following command, switching out “site.url” for your websites domain name:

```
nano /etc/nginx/common/site.url-wpfc.conf
```

For example:

```
nano /etc/nginx/common/yourwebsite.com-wpfc.conf
```

You can now make your edits. Use your down arrow key to navigate to the bottom of the file. You will see the following block of code, and the line we need to edit is red:

```
location ~ \.php$ {  try_files $uri =404;  fastcgi_cache_bypass $skip_cache;  fastcgi_no_cache $skip_cache;  fastcgi_cache FASTCGICACHE;  more_set_headers 'X-Grid-Cache-TTL $cache_ttl';  more_set_headers 'X-Grid-Cache-Skip $skip_reason';  more_set_headers 'X-Grid-Cache $upstream_cache_status';  set $http_x_accel_expires $cache_ttl;  fastcgi_split_path_info ^(.+\.php)(.*)$;  include fastcgi_params;  include /etc/nginx/extra.d/php-context.conf;  include /var/www/ngx.com/nginx/*-php-context.conf;  #fastcgi_param HTTPS on;  fastcgi_pass unix:/var/run/php/php73-fpm-ngx.com.sock;  #http2_push_preload on;}
```

Here we need to remove the $= 404 from the try_files directive and replace it with $uri/ /index.php?$args, like so:

```
location ~ \.php$ {  try_files $uri $uri/ /index.php?$args;  fastcgi_cache_bypass $skip_cache;  fastcgi_no_cache $skip_cache;  fastcgi_cache FASTCGICACHE;  more_set_headers 'X-Grid-Cache-TTL $cache_ttl';   more_set_headers 'X-Grid-Cache-Skip $skip_reason';  more_set_headers 'X-Grid-Cache $upstream_cache_status';  set $http_x_accel_expires $cache_ttl;  fastcgi_split_path_info ^(.+\.php)(.*)$;  include fastcgi_params;  include /etc/nginx/extra.d/php-context.conf;  include /var/www/ngx.com/nginx/*-php-context.conf;  #fastcgi_param HTTPS on;  fastcgi_pass unix:/var/run/php/php73-fpm-ngx.com.sock;  #http2_push_preload on;}
```

Save the file with CTRL+O, and then Enter. Exit nano with CTRL+X.

You can now move on to step 4.

 

### PHP: Edit the site.url-php.conf

Open the file in the nano editor with the following command, switching out “site.url” for your websites domain name:

```
nano /etc/nginx/common/site.url-php.conf
```

For example:

```
nano /etc/nginx/common/yourwebsite.com-php.conf
```

You can now make your edits. Use your down arrow key to navigate to the bottom of the file. You will see the following block of code, and the line we need to edit is red:

```
location ~ \.php$ {  #modsecurity_rules_file /etc/nginx/modsec/main.conf;  try_files $uri =404;  fastcgi_split_path_info ^(.+\.php)(.*)$;  include fastcgi_params;  include /etc/nginx/extra.d/php-context.conf;  include /var/www/ngx.com/nginx/*-php-context.conf;  #fastcgi_param HTTPS on;  fastcgi_pass unix:/var/run/php/php73-fpm-ngx.com.sock;  #http2_push_preload on;}
```

Here we need to remove the $= 404 from the try_files directive and replace it with $uri/ /index.php?$args, like so:

```
location ~ \.php$ {  #modsecurity_rules_file /etc/nginx/modsec/main.conf;  try_files $uri $uri/ /index.php?$args;  fastcgi_split_path_info ^(.+\.php)(.*)$;  include fastcgi_params;  include /etc/nginx/extra.d/php-context.conf;  include /var/www/ngx.com/nginx/*-php-context.conf;  #fastcgi_param HTTPS on;  fastcgi_pass unix:/var/run/php/php73-fpm-ngx.com.sock;  #http2_push_preload on;}
```

Save the file with CTRL+O, and then Enter. Exit nano with CTRL+X.

You can now move on to step 4 below.

 

## Step 4. Ensure Your Changes Persist

The last step is to make these changes persist. Without this, your changes may be lost in the future and your redirects will cease to work.

First, ensure sure the _custom directory exists with:

```
mkdir /etc/nginx/common/_custom
```

Then run the following command, switching out “site.url-{cachetype}.conf” for the file you’ve just been editing:

```
cp /etc/nginx/common/site.url-{cachetype}.conf /etc/nginx/common/_custom/
```

For example, if you’re using Redis caching it would look like this:

```
cp /etc/nginx/common/yourwebsite.com-wp-redis.conf /etc/nginx/common/_custom/
```

 

## Step 5. Check and Reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

Your setup is now complete! Please be sure to test your redirects to confirm that they’re working correctly.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

