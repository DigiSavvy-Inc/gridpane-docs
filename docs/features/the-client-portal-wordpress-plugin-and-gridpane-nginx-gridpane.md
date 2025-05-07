# The Client Portal WordPress Plugin and GridPane Nginx | GridPane

# The Client Portal WordPress Plugin and GridPane Nginx

 

3 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

## Introduction

If you’re using the Client Portal WordPress plugin, you’ll see a message in your dashboard that says:

 

Because your server is running on Nginx, we cannot use the .htaccess file to protect your private files.Please add the following rules to your Nginx config to disable direct file access:

```
location ~ ^/wp-content/uploads/leco-cp/(.*)$ { rewrite / permanent; }
```

You can usually ask your hosting service to help you with it. If you’re pretty sure the rules have been added, you can dismiss this message.

 

In our testing, the above code didn’t actually work as intended. It will return a 403 for the filepath above, but any private files inside /leco-cp/ will still be accessible when not logged in. We’ve modified it to only allow access to private files when logged into the website, and we’ve also reached out to the plugin author with our findings.

UPDATE: The above code is now their most recent updated recommendation. We had a brief correspondence with their team awhile back but haven’t tested this yet. For now, we still recommend you use our code below.

Below will walk you through how to add this to your server.

## Step 1. SSH into your server:

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Create a config for Client Portal

We’ll be creating a file called “clientportal-main-context.conf”. Run the following command switching out “site.url” for your website’s domain:

```
nano /var/www/site.url/nginx/clientportal-main-context.conf
```

Paste the following [modified] code into the file:

```
location ~* ^/wp-content/uploads/leco-cp/.*$ {rewrite / permanent;
allow 127.0.0.1;
deny all;
return 403;
}
```

The above code ensures that when logged in, private files can be downloaded.When not logged in, it will return a 403 forbidden error.

Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

 

## Step 3. Check and Reload Nginx

We now need to test our nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

Your Client Portal plugin setup is now complete!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

