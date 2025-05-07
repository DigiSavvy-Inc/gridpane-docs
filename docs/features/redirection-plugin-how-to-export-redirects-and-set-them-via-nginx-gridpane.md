# Redirection Plugin: How to export redirects and set them via Nginx | GridPane

# Redirection Plugin: How to export redirects and set them via Nginx

 

2 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

## Intro

Redirection is an excellent plugin that also comes with the functionality to export your redirects as Nginx rewrite rules (which is fancy talk for server-level redirects). You can use the plugin interface to build your redirects, export them, and add them at the server level as an include for better performance.

It’s great for catching URL changes on busy websites, as you can set up Redirection to automatically recreate redirects for posts/pages/custom post types as needed, and then add them in Nginx in batches as time goes by.

If you don’t already have it installed, you can view/download the plugin for free here:https://wordpress.org/plugins/redirection/

 

## Step 1. Export Your Redirects

To export your redirects and add them to your GridPane server directly, log into your website and head to the Redirection page and click on “Import/Export” at the top.

Select “WordPress redirects” and “Nginx rewrite rules” from the dropdowns and click view:

Here you can either download them or simply leave the page open and copy and paste them in step 3.

 

## Step 2. SSH into your server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 3. Create redirect-main-context.conf

We now need to create a file called redirect-main-context.conf inside /var/www/site.url/nginx and add your exported redirection code. Create the file with the following command (switching out site.url for your domain name):

```
nano /var/www/site.url/nginx/redirect-main-context.conf
```

Next copy and paste your rewrites only (and also the Redirection info as well if you wish – the date may come in handy).

Important: If the rewrites are added inside server { } it will result in an Nginx syntax error.

```
# Created by Redirection# Tue, 08 Dec 2020 18:33:41 +0000# Redirection 4.9.2 - https://redirection.merewrite ^/test-example$ /sample-page permanent;rewrite ^/another-example$ https://domain.com permanent;# End of Redirection
```

Now Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

 

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

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

