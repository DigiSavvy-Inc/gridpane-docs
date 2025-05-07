# Allow or Deny IP Addresses on OpenLiteSpeed | GridPane

# Allow or Deny IP Addresses on OpenLiteSpeed

 

3 min read 

## Introduction

GridPane OpenLiteSpeed (OLS) offers a server-wide and per-site, IP allow/deny mechanism. This allows you to explicitly allow or deny access to a list of IP addresses and/or subnets to your virtual hosts (which in this context means each of your individual websites).

Below we’ll look at how you use these configuration files on your OLS servers. You’ll need to connect to your server over SSH or SFTP to edit these files. Please see the guides linked below to get started.

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Three Quick Notes

 

## Allow IP Addresses

There are two individual configurations, one that applies server-wide, and one that is site-specific.

The server-wide configuration is located here:

```
/usr/local/lsws/conf/ip_allow.conf
```

The site-specific config is located here (replace “site.url” with your domain name):

```
/var/www/site.url/ols/ip_allow.conf
```

### Add Your IP/s

To edit either file, open them with nano like so:

```
nano /usr/local/lsws/conf/ip_allow.confnano /var/www/site.url/ols/ip_allow.conf
```

Add one IP address or subnet per line, then hit CTRL+O followed by Enter to save the file, and CTRL+X to exit nano.

### Restart OLS

For the changes to take effect you will first need to restart OLS.

If you’ve made server-wide changes, restart and regenerate the server configuration with the following command:

```
gpols httpd
```

If you’ve made site-specific changes restart and regenerate the website configuration with this command (replace “site.url” with your domain name):

```
gpols site site.url
```

Your rule is now in place.

 

## Deny IP Addresses

When denying IPs at the server level it will close its connection so nothing gets hit on the server. If you deny at the site level, a 403 HTTP Error will be served.

Like above, there are two individual configurations, one that applies server-wide, and one that is site-specific.

The server-wide configuration is located here:

```
/usr/local/lsws/conf/ip_deny.conf
```

The site-specific config is located here (replace “site.url” with your domain name):

```
/var/www/site.url/ols/ip_deny.conf
```

### Add Your IP/s

To edit either file, open them with nano like so:

```
nano /usr/local/lsws/conf/ip_deny.confnano /var/www/site.url/ols/ip_deny.conf
```

Add one IP address or subnet per line, then hit CTRL+O followed by Enter to save the file, and CTRL+X to exit nano.

### Restart OLS

For the changes to take effect you will first need to restart OLS.

If you’ve made server-wide changes, restart and regenerate the server configuration with the following command:

```
gpols httpd
```

If you’ve made site-specific changes restart and regenerate the website configuration with this command (replace “site.url” with your domain name):

```
gpols site site.url
```

Your rule is now in place.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

