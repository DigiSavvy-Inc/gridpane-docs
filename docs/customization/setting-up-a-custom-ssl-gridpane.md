# Setting up a Custom SSL | GridPane

# Setting up a Custom SSL

 

5 min read 

In some cases, you may want to run a custom non Let’s Encrypt based SSL. This article will walk you through how to do this on GridPane.

 

 

### Important

Custom SSLs are not supported by GridPane.
Once you completed your setup, do NOT use our SSL toggles as this will interfere with your custom SSL and may cause issues on your live website.

## Introduction

Setting up a custom SSL on GridPane servers requires some manual work on the command line. Before we begin, it’s useful to understand a little about Virtual Hosts (also known as Virtual Servers) and how they work.

### Virtual Host Files

Virtual host (vhost) files are individual website configuration files that, by implementing them, allow you to host more than one website on a server, assigning each website to its own separate directory.

On Nginx, this actually implemented via a server block, but the terms vhost, virtual host, and virtual servers are still the commonly used terms. If you’re ever reading up or watching videos on Nginx and you hear these terms, this is what they all refer to.

These configuration files contain details of how to serve your websites, including all of our custom Nginx configs, what port to serve it from (80 for HTTP, 443 for HTTPS), and where to look up your SSL certificate.

 

### Getting Started

To set up your custom SSL you will need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 1. Create the SSL folder

First, you need to create the folder where your certificates are going to be stored with the following command, replacing “site.url” with your domain name:

```
mkdir /etc/nginx/ssl/site.url
```

For example:

```
mkdir /etc/nginx/ssl/gridpane.com
```

### Add/Upload your SSL

Add your custom SSL certificates to the server.

### Converting crt and key files

If your custom certificates are in crt format, you will need to convert them with the following (replacing “site.url” with your domain):

```
openssl x509 -in /path/to/cert.crt -out /etc/nginx/ssl/site.url/cert.pem
```

And if you have a .key files you will need to convert it with the following (replacing “site.url” with your domain):

```
openssl rsa -in /path/to/key.key -out /etc/nginx/ssl/site.url/key.pem
```

 

## Step 2. Setup the correct Virtual Host file

Now that your website has been configured we need to create the correct vhost for your website. Before we create the vhost, we need 2 pieces on information: –

### 1. Check the configuration type

For the configuration type run the following command (replacing site.url for your domain name):

```
gp conf -ngx -type-check site.url -q
```

### 2. Check the caching type

For the caching type run the following command (replacing site.url for your domain name):

```
gp conf -ngx -cache-check site.url -q
```

### 3. Generate your https vhost

Now you have the two pieces of info that we need, and we’ll be changing to type from http to https. The output from the above two commands will look similar to this:

```
root@dev-ngx1:~# gp conf -ngx -type-check yourdomain.com -qhttp-rootroot@dev-ngx1:~# gp conf -ngx -cache-check yourdomain.com -qredis
```

The routing and caching type may differ. You’ll be copying and pasting them, but adding add “s” to the end of http.

The command to generate your new vhost follows this format:

```
gp conf -ngx -generate $config_type $cache_type site.url
```

So, in this case, we need to generate a https-root redis config like this:

```
gp conf -ngx -generate https-root redis yourdomain.com
```

If generating for a wildcard SSL, it would look as follows:

```
gp conf -ngx -generate https-wildcard redis yourdomain.com
```

 

## Step 3. Activate the SSL Certificate

Now we need to activate the SSL. However, before you do that, first check that the Nginx syntax is all good with:

```
nginx -t
```

If there are any errors it will let you know. These will need to be fixed before reloading Nginx. This is very important.

If everything is OK, reload nginx using the following command:

```
gp nginx reload
```

Do not toggle on SSL on the Gridpane Panel.

 

## Step 4. GPOCSP Stapling

You may see GPOCSP related warnings when reloading Nginx. For example:

```
Jan 01 01:01:00 servername gpocsp[22675]: 140173244732544:error:02001002:system library:fopen:No such file or directory:../crypto/bio/bss_file.c:69:fopen('/root/gridenv/acme-wildcard-configs/site.url/site.url/ca.cer','r')
```

The GPOCSP function checks for the .cer file to find the OCSP responder URL based on whether it is on the certbot path or the ACME path based on the file path.

/etc/nginx/ssl/site.url/cert.pem is the file path for the installation of ACME certs, while the original .cer file lives in the path in the error.

If you have installed your own custom certs and the GPOCSP function can’t find the original .cer file when it looks and is throwing this error, you have 2 options: –

This is important as this error may prevent the stapling of other domains on the server.

### Option 1. Add the .cer file

First, create the directories with  the following command (replacing the two “site.url“s with your domain name):

```
mkdir -p /root/gridenv/acme-wildcard-configs/site.url/site.url/
```

Now add .cer file and name it “ca.cer” so it’s file path is:

```
/root/gridenv/acme-wildcard-configs/site.url/site.url/ca.cer
```

### Option 2. Exclude your website

Create a file called “gpocsp.exclude” in the root directory with the following command:

```
nano /root/gpocsp.exclude
```

Now in the nano editor, simply type your domain name. Save the file with CTRL+O and then Enter. Exit nano with CTRL+X.

Check all is well with:

```
gpocsp
```

It will be obvious if there’s still an issue. If it’s all good it will look like this:

```
root@dev-ngx1:/var/www/dev.domain.com/logs# gpocsp0 - /etc/nginx/ssl/examplewebsite.com/cert.pem: goodThis Update: Jul 2 21:00:00 2021 GMTNext Update: Jul 9 21:00:00 2021 GMT0 - /etc/letsencrypt/live/upmafghkjhdmm.gridpanevps.com/fullchain.pem: goodThis Update: Jul 3 03:00:00 2021 GMTNext Update: Jul 10 03:00:00 2021 GMT0 - /etc/letsencrypt/live/upmafghkjdhmmstat.gridpanevps.com/fullchain.pem: goodThis Update: Jul 4 14:00:00 2021 GMTNext Update: Jul 11 14:00:00 2021 GMT
```

 

 

### Important

As expressed at the beginning of this article, after making these changes please do NOT use our SSL toggles, otherwise, you will have to repeat the above process.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

