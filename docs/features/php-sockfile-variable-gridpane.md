# PHP Sockfile Variable | GridPane

# PHP Sockfile Variable

 

4 min read 

## Introduction

This article will provide some background on Nginx and PHP-FPM configuration, and specifically how sockfiles work on your Nginx servers.

We’ll also look at how to create PHP specific configurations ensure any they persist when changing your websites PHP version.

 

## Nginx, PHP-FPM and .sock Files

Nginx doesn’t run its own server-side language processors for languages such as PHP. This being the case, we need to instead run PHP as its own microservice “PHP-FPM” (FPM stands for FastCGI Process Manager) to be able to host websites that run on PHP and handle any PHP requests.

When a request comes in that requires PHP processing, Nginx will pass this to PHP-FPM, this will be processed to generate what is the equivalent of the static HTML version of the page and pass it to Nginx, which then returns it to the client (for example, the visitor’s browser).

For this to work, Nginx and PHP-FPM need to be able to transfer data back and forth.

### How Nginx Connects to PHP-FPM

To connect Nginx and PHP-FPM, PHP-FPM listens for requests from FastCGI on a UNIX domain socket. Nginx uses this socket to pass requests to PHP-FPM via the fastcgi_pass directive.

Here’s an example of a location block that will receive and process PHP requests:

```
location ~ \.php$ {
   try_files $uri =404;
   fastcgi_split_path_info ^(.+\.php)(.*)$;
   include fastcgi_params;
   include /etc/nginx/extra.d/*php-context.conf;
   include /var/www/example.com/nginx/*-php-context.conf;
   fastcgi_pass unix:/var/run/php/php73-fpm-example.com.sock;
}
```

Here we see the pass to the UNIX php73-fpm-example.com.sock file, which is specific to PHP 7.3.

### PHP Version Matters

As each individual version of PHP (7.2, 7.3, 7.4 etc) has its own sock file, this is where the $sockfile variable comes in.

Below we will look at how this works on GridPane, and how you can use it to ensure that if you add your own PHP location blocks, they are not going to need re-creating or cause PHP-FPM to go down if you change your website’s PHP version.

 

## The $sockfile Variable

As each version of PHP has its own unique sock file, whenever a websites PHP version is changed, all Nginx configuration files that use it previously had to be regenerated in order to rewrite the current PHP sock file into place on every fastcgi_pass directive.

The $sockfile variable means that now only one file needs to be regenerated, which has numerous benefits, including ensuring your own PHP location blocks persist when changing PHP versions, and that PHP-FPM isn’t accidentally taken down by overlooking previously created configs.

### How it Works

Inside your websites, virtual hosts file exists the following include:

```
include /var/www/test.com/nginx/*example.com-sockfile.conf;
```

Side note: You can view your own websites’ virtual host with the following command (switching out site.url for your own domain name):

```
gp conf nginx show site.url
```

Inside the file that matches this wildcard, we store the UNIX sock file into an Nginx variable using the Nginx directive set_if_empty. For example:

```
set_if_empty $sockfile unix:/var/run/php/php73-fpm-example.com.sock;
```

Now, when the PHP version for a website changes we update this single file.

Now this is stored that in a variable, it simplifies the Nginx configuration templates and they no longer need their fastcgi_pass directive input value editing. Instead, they are static like so:

```
location ~ \.php$ {...   set_if_empty $sockfile php;   fastcgi_pass $sockfile;...}
```

Here we are using set_if_empty again so that if the sock file config doesn’t exist it will set to the default server PHP upstream socket.

The set_if_empty is just insurance though, and the UNIX socket is now passed via the variable $sockfile when it does exist.

 

## Creating PHP Location Blocks

The $sockfile variable allows us to set up our own PHP Location blocks without ever needing to worry about switching PHP versions down the line.

Here’s an example to show this in action.

### Hypothetical

You want to use our block PHP execution in the /wp-content directory security measure, with the exception of one specific plugin file.

### Step 1. Create the Configuration File

Inside the block wp-content PHP execution security measure, there is this include that we can use to add out location block: /var/www/site.url/nginx/*-before-disable-wp-content-php-main-context.conf. Learn more about the additional measure security plugins here:

Additional Security Measure Nginx Includes

Create the file with the following command (replacing “site.url” with your domain name and “pluginname” with a name that makes sense for you):

```
nano /var/www/site.url/nginx/pluginname-before-disable-wp-content-php-main-context.conf
```

### Step 2. Add your Location Block

Add the following to the file, switching out the example plugin file path with your own:

```
location ~ /wp-content/plugins/dirty-dirty-plugin/file.php$ {  try_files $uri =404;  fastcgi_split_path_info ^(.+\.php)(.*)$;  include fastcgi_params;  set_if_empty $sockfile php;  fastcgi_pass $sockfile;}
```

As we’re using the $sockfile variable, if we change the websites PHP version this configuration will persist and call the correct PHP .sock file.

Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

### Step 3. Check and Reload Nginx

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

