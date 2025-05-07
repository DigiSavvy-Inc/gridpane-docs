# Protecting files in Easy Digital Downloads on GridPane | GridPane

# Protecting files in Easy Digital Downloads on GridPane

 

2 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

When using Easy Digital Downloads on Nginx you’ll get a notification inside your website that says: –

—

The download files in /var/www/site.url/htdocs/wp-content/uploads/edd are not currently protected due to your site running on NGINX.

To protect them, you must add a redirect rule as explained in this guide.

If you have already added the redirect rule, you may safely dismiss this notice

https://docs.easydigitaldownloads.com/article/682-protected-download-files-on-nginx

—

To do this, you first need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 1. Create a file named edd-main-context.conf

First, begin by creating the edd-main-context.conf file, replacing “site.url” with your domain name:

```
nano /var/www/site.url/nginx/edd-main-context.conf
```

## Step 2. Add this to the contents to the file

```
location ~ ^/wp-content/uploads/edd/(.*?).zip$ { rewrite / permanent; }

rewrite ^/wp-content/uploads/edd/(.*).zip$ / permanent;
```

Save the file with CTRL+O, and then Enter. Exit nano with CTRL+X.

## Step 3. Check the syntax of nginx.conf

```
nginx -t
```

If, after entering the above command, you see a message letting you know that everything’s OK:

```
nginx: the configuration file /etc/nginx/nginx.conf syntax is oknginx: configuration file /etc/nginx/nginx.conf test is successful
```

You can now you can reload Nginx by running

```
gp ngx reload
```

Your Easy Digital Download files will now be protected.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

