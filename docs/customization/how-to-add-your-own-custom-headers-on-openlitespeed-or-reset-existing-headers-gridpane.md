# How to add your own custom headers on OpenLiteSpeed (or reset existing headers) | GridPane

# How to add your own custom headers on OpenLiteSpeed (or reset existing headers)

 

2 min read 

## Introduction

Adding your own custom headers to your WordPress websites on OpenLiteSpeed (OLS) servers is quick and simple. Each of your websites has the following directory:

```
/var/www/site.url/ols/
```

Here you’ll find the headers.conf file, which is where you’ll find your website’s default security headers, and where you can add your own custom headers as well.

You don’t need to worry about the headers you add here getting overwritten, and if any of the default headers don’t fit your needs, you can remove them or comment them out using a hashtag at the beginning of the line.

### Limitation vs Nginx

One limitation with OpenLiteSpeed compared to Nginx is that you can’t add a server-wide custom header on OLS. Each site needs to be edited individually.

Fortunately though, the use case for this is quite rare, and adding headers is easy.

 

## Formatting

The default headers.conf contains the following:

```
# Custom User Headers
# Usage: one line per entry
# Included in /usr/local/lsws/conf/vhosts/site.url/vhconf.conf
Referrer-Policy strict-origin-when-cross-origin
Strict-Transport-Security: max-age=31536000
X-Content-Type-Options nosniff
X-Frame-Options SAMEORIGIN
X-XSS-Protection 1; mode=block
```

Each header you add must be on its own line.

The header name should contain no spaces, and there should be a space between the name and the value. For example:

```
Steve-Hosted True
```

For more than value, separate them with a semi-colon like so:

```
Steve-Hosted True; Package-Name
```

You can also wrap multiple values in quotes as well:

```
Steve-Hosted "True; Package-Name"
```

Here’s an example of what some custom headers (a bunch of nonsense) I’ve added to a test website look like:

 

## Adding Your Custom Header/s

### Step 1. SSH into your server

To get started you’ll first need to connect to your server via SSH. Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Add your header/s

Edit the headers.conf with the following command (replace “site.url” with your domain name):

```
nano /var/www/site.url/ols/headers.conf
```

Add each of your headers on their own line, then hit Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.

### Step 3. Rebuild Your vhconf

As the rewrites.conf file has been modified, a specific OpenLiteSpeed command has to be executed in order for the changes to take effect (replace “site.url” with your domain name):

```
gpols site site.url
```

 

## Checking Your Custom Header/s

If you know what this is, you don’t require a tutorial on how to check it, so we’ll skip this part.

One thing to be aware of, depending on what you’ve edited, is that previous headers may be cached by your browser and/or the server, and you may need to clear the cache and check the site in an incognito window to confirm the changes are in fact live on the website.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

