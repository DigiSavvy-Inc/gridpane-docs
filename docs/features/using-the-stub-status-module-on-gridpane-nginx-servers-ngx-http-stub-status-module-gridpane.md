# Using the stub_status module on GridPane Nginx Servers (ngx_http_stub_status_module) | GridPane

# Using the stub_status module on GridPane Nginx Servers (ngx_http_stub_status_module)

 

2 min read 

### Table of Contents

 

## Introduction

The ngx_http_stub_status_module module provides access to basic status information. On GridPane this is installed and enabled by default, and ready to use for any use cases you have that requires it.

You can learn more about it directly over in the official Nginx documentation here:

Module ngx_http_stub_status_module

### Module Check

You can confirm this is active on your server by checking for the --with-http_stub_status_module configuration parameter. Run the following command:

```
nginx -V 2>&1 | grep -o with-http_stub_status_module
```

This will return the following output:

```
root@nginx:# nginx -V 2>&1 | grep -o with-http_stub_status_module
with-http_stub_status_module
```

### Using stub_status;

Below we’ll look at how you can use the stub_status; on your websites. If this is the first time connecting to your servers, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 1. Activate stub_status;

We can place the stub_status; location in a *-main-context.conf file on either a specific site, or for all websites on your server.

### Option 1. Create a site-specific config

If you only want to add stub_status; to a specific site, run the following command, switching out site.url for your website’s URL:

```
nano /var/www/site.url/nginx/stub-status-main-context.conf
```

### Option 2. Create a server-wide config

To add this to every site on a server, run the following command:

```
nano /etc/nginx/extra.d/stub-status-main-context.conf
```

### Add your configuration

In that file, specific the URI where you want to add the stub_status;. Here’s an example:

```
location = /nginx_status {
stub_status;
}
```

The /nginx_status can be any URI that makes sense for you.

Save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

 

## Step 2. Check and reload Nginx

Test your Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

```
gp ngx reload
```

 

## Step 3. Check your work

To check its activation visit: yourwebsitehere.com/nginx_status (or whatever URI you entered as the location in your config).

Here you’ll see something that looks as follows:

```
Active connections: 1
server accepts handled requests
163 163 50
Reading: 0 Writing: 1 Waiting: 0
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

