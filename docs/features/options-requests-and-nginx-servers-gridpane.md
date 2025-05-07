# OPTIONS Requests and Nginx Servers | GridPane

# OPTIONS Requests and Nginx Servers

 

2 min read 

## Introduction

GridPane allows OPTIONS requests out of the box, so plugins such as Prestoplayer will work by default on your servers.

However, if you’re using a plugin that requires OPTIONS with a CDN, you may need to add a request header for it to be able to communicate with your site. This article will walk you through that process.

To get started you will need to connect to your server. Please see the following guides to get started if this if your first time connecting to a GridPane server:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Edit the headers-http-context.conf

We need to edit this file to implement the change. Run the following command to open it in the nano editor:

```
nano /etc/nginx/extra.d/headers-http-context.conf
```

The contents of the config looks like this:

```
# ## GridPane HTTP Header includes...# User updates here will stick server wide.# Version 1.2.0# ##more_set_headers "allow: GET, POST, HEAD, PURGE, OPTIONS" always;#if ($request_method !~ ^(GET|POST|HEAD|PURGE|OPTIONS)$) {#return 405;#}
```

Remove the hashtags at the beginning of the last 4 lines (starting from “#more_set_headers”), so the file looks like this:

```
# ## GridPane HTTP Header includes...# User updates here will stick server wide.# Version 1.2.0# #more_set_headers "allow: GET, POST, HEAD, PURGE, OPTIONS" always;if ($request_method !~ ^(GET|POST|HEAD|PURGE|OPTIONS)$) {return 405;}
```

Now save the file with CTRL+O followed by Enter, then exit nano with CTRL+X.

This adds a response header to your website, and explicitly states that

### Check and Reload Nginx

We now need to check if the conf files are correct then reload Nginx.

Test your nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

 

## Confirm Your Work

Head over to your website and right-click > Inspect. Click through to the network page and reload the page.

On the left, select the URL and then you’ll be able to confirm the response headers are now active:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

