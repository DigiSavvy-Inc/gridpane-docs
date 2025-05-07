# How to Configure OpenLiteSpeed (OLS) Log Settings and Retention | GridPane

# How to Configure OpenLiteSpeed (OLS) Log Settings and Retention

 

7 min read 

## Introduction

The GridPane OpenLiteSpeed (OLS) stack offers the ability to adjust how your website error and access logs are configured on the server. This includes the size they’re allowed to grow to before being rotated, and how long they are retained for.

By default, we configure these settings out of the box to ensure that servers with very high-traffic websites don’t create logs that quickly fill up a server’s disk space and take it offline. This article details how to configure these settings.

### Table of Contents

 

## Definitions

Below you’ll find a definition for terms used in this article. You can also learn more in the official LiteSpeed documentation here:

https://www.litespeedtech.com/docs/webserver/config/slog

### Keep Days

### Rolling Size

### Log Level

### Debug Level

 

## Part 1. Error Logs

OpenLiteSpeed error logs don’t have functioning directives for keepDays or compression. However, at GridPane these can be customized via our ols-max-error-log-count and ols-max-error-log-count settings via GP-CLI – details in section 1.3 below.

 

## 1.1. Adjust Error Log Settings for Entire Server

### Default Server Settings

GridPane sets the following defaults:

```
errorlog logs/error.log {
logLevel DEBUG
debugLevel 0
rollingSize 10M
enableStderrLog 1
}
```

### Customize rollingsize, loglevel, and debuglevel

Use the following GP-CLI commands to adjust the Server httpd level via ENV:

```
gp conf write ols-error-log-rollingsize {{integer}}M 
gp conf write ols-error-log-loglevel DEBUG||ERROR
gp conf write ols-error-log-debuglevel {{integer:1-10}}
```

Replace {{integer}} with a whole number. For example:

```
gp conf write ols-error-log-rollingsize 15M gp conf write ols-error-log-loglevel DEBUGgp conf write ols-error-log-debuglevel 3
```

### Regenerate the httpd config

To set your changes live, regenerate the httpd config with:

```
gp ols httpd
```

 

## 1.2. Adjust Error Log Settings for Individual Websites

### Site Defaults

GridPane sets the following site defaults:

```
errorlog $VH_ROOT/logs/site.url.error.log {useServer 0logLevel DEBUGrollingSize 10MkeepDays 7}
```

### Customize rollingsize and loglevel

```
gp conf write ols-error-log-rollingsize {{integer}}M -site.env {{site.domain}}gp conf write ols-error-log-loglevel DEBUG||ERROR -site.env {{site.domain}}
```

Replace {{integer}} with a whole number and {{site.domain}} with your website URL. For example:

```
gp conf write ols-error-log-rollingsize 15M -site.env mywebsite.comgp conf write ols-error-log-loglevel ERROR -site.env mywebsite.com
```

### Regenerate the vhconf

Finally, regenerate the site.url/vhosts/vhconf config with:

```
gp ols site {{site.domain}}
```

 

## 1.3. Adjust Error Log Retention Settings

As mentioned, OLS does not have anything for compression or rotating the error log files, so instead, at GridPane you can adjust these ENV values:

### 1.3.1. Current Defaults

The following defaults are set by GridPane:

```
ols-max-error-log-count:3
ols-max-error-log-archive-count:7
```

 

### 1.3.2. Adjust httpd Server logs

You can adjust these defaults for all websites on a server using the following GP-CLI:

```
gp conf write ols-max-error-log-count {{integer}}
gp conf write ols-max-error-log-archive-count {{integer}}
```

Replace {{integer}} with a whole number. As an example, the following sets compression to begin at day 7, and files older than 30 days will be automatically deleted:

```
gp conf write ols-max-error-log-count 7 
gp conf write ols-max-error-log-archive-count 30
```

### Regenerate the httpd config

To set your changes live, regenerate the httpd config with:

```
gp ols httpd
```

 

### 1.3.3. Adjust vhconf Site logs

```
gp conf write ols-max-error-log-count {{integer}} -site.env {{site.domain}}
gp conf write ols-max-error-log-archive-count {{integer}} -site.env {{site.domain}}
```

Replace {{integer}} with a whole number and {{site.domain}} with your website URL. As an example, the following applies to one specific site and sets compression to begin at day 5, and files older than 21 days will be automatically deleted:

```
gp conf write ols-max-error-log-count 5 -site.env mywebsite.comgp conf write ols-max-error-log-archive-count 21 -site.env mywebsite.com
```

### Regenerate the vhconf

Finally, regenerate the site.url/vhosts/vhconf config with:

```
gp ols site {{site.domain}}
```

 

## Part 2. Access Logs

For access logs, we have the following directives we can manage via ENV: rollingSize, keepDays, compressArchive.

### Access Log Defaults

GridPane sets the following default settings:

```
accesslog logs/access.log {
rollingSize 10M
keepDays 30
compressArchive 1
}
```

 

## 2.1. Adjust Access Log Settings for Entire Server

You can adjust the log settings for all websites on the server at the httpd level with the following GP-CLI:

```
gp conf write ols-access-log-rollingsize {{integer}}M 
gp conf write ols-access-log-keepdays {{integer}}
gp conf write ols-log-compressarchive 1||0
```

Replace {{integer}} with a whole number. For example:

```
gp conf write ols-access-log-rollingsize 15Mgp conf write ols-access-log-keepdays 30gp conf write ols-log-compressarchive 1
```

### Regenerate the httpd config

To set your changes live, regenerate the httpd config with:

```
gp ols httpd
```

 

## 2.2. Adjust Access Log Settings for Individual Websites

You can adjust the log settings for individual websites at the vhconf level with the following GP-CLI:

```
gp conf write ols-access-log-rollingsize {{integer}}M -site.env {{site.domain}}
gp conf write ols-access-log-keepdays {{integer}} -site.env {{site.domain}}
gp conf write ols-log-compressarchive 1||0 -site.env {{site.domain}}
```

Replace {{integer}} with a whole number and {{site.domain}} with your website URL. For example:

```
gp conf write ols-access-log-rollingsize 15M -site.env mywebsite.com
gp conf write ols-access-log-keepdays 30 -site.env mywebsite.com
gp conf write ols-log-compressarchive 1 -site.env mywebsite.com
```

We recommend that you always keep compressing archives active, but you can choose not to if you wish.

### Regenerate the vhconf

Finally, regenerate the site.url/vhosts/vhconf config with:

```
gp ols site {{site.domain}}
```

 

## 2.3. Adjust Access Log Format Pattern (Individual Websites Only)

At the website level, logFormat can also be adjusted for the access log using an include.

### Log Format Default

GridPane site defaults are like so:

```
accesslog $VH_ROOT/logs/site.url.access.log {
useServer 0
logFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\"
logHeaders 7
rollingSize 10M
keepDays 30
compressArchive 1
}
```

### Customize Log Format

If you want to customize the log format, you can add your pattern to the access_log_format.conf include.

Run the following command to create the config (replacing site.url with your website’s URL):

```
nano /var/www/site.url/ols/access_log_format.conf
```

Add your pattern, for example:

```
%t %h %l %u "%r" %>s %b "%{Referer}i" "%{User-agent}i"
```

Save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

### Regenerate the vhconf

Finally, regenerate the site.url/vhosts/vhconf config with:

```
gp ols site {{site.domain}}
```

 

## 2.4. Adjust Access Log Retention Settings

Since access logs do have the rotation on size, days, and compression, there is less need for management of the archive count. For this reason, we do not set this by default.

However, while it is unlikely to be needed for most servers, it is available if you have sites with extremely high traffic and need to get log size under control.

 

### 2.4.1 Server-Level Log Rotation

Use the following command to set the log retention for all sites on a server:

```
gp conf write ols-max-access-log-archive-count {{integer}}
```

Replace {{integer}} with a whole number. For example:

```
gp conf write ols-max-access-log-archive-count 30
```

### Regenerate the httpd config

To set your changes live, regenerate the httpd config with:

```
gp ols httpd
```

 

### 2.4.2. Site Level Log Rotation

Use the following command to set the log retention for a specific website:

```
gp conf write ols-max-access-log-archive-count {{integer}} -site.env {{site.domain}}
```

Replace {{integer}} with a whole number and {{site.domain}} with your website URL. For example:

```
gp conf write ols-max-access-log-archive-count 30 -site.env mywebsite.com
```

### Regenerate the vhconf

Next, regenerate the site.url/vhosts/vhconf config with:

```
gp ols site {{site.domain}}
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

