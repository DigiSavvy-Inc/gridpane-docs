# Getting Started with GridPane OpenLiteSpeed (OLS) | GridPane

# Getting Started with GridPane OpenLiteSpeed (OLS)

 

6 min read 

### Table of Contents

 

## An Introduction to OLS

This article is a quick introduction to our OpenLiteSpeed stack along with links to relevant articles for more information.

### About OpenLiteSpeed

OpenLiteSpeed is the Open Source edition of LiteSpeed Web Server Enterprise. OLS contains all of the essential features found in LiteSpeed Enterprise, plus our own additions like our Firewall integrations, security hardening features, Fail2Ban, CLI, and more.

### Apache Replacement

OLS isn’t a drop-in replacement for Apache like LiteSpeed Enterprise, but moving your WordPress websites from hosts running on Apache to servers running OpenLiteSpeed is a straightforward task and plugins that work on Apache should work seamlessly.

### PHP

LiteSpeed and OpenLiteSpeed run PHP LiteSpeed SAPI (PHP LSAPI), which is a custom version of PHP specific to LiteSpeed Web Servers. It is designed specifically for high performance.

### Performance

OLS uses event-driven architecture and has the capability of serving thousands of clients simultaneously while expending very minimal CPU, memory, and other resources.

Like Nginx, it offers excellent performance and is perfect for websites with a lot of traffic.

### Security

OLS has built-in anti-DDoS security, Anti-DDoS connection and bandwidth throttling, Anti SSL BEAST and negotiation attack capabilities, strict HTTP request validation, denies buffer-overrun attempts, mod_security compatibility, and SSL client verification.

While it doesn’t directly offer brute force protection for WordPress websites, GridPane OLS of course comes with our Fail2Ban integration, both for /wp-login.php and /xmlrpc.php protection, and the WPFail2Ban plugin integration. Fail2Ban also has the added benefit of keeping a lot of worthless bad bot traffic off your server.

 

## .htaccess

OpenLiteSpeed comes with a .htaccess file that supports Apache mod_rewrite rules, but it is recommended to add your custom rewrite rules to the auto-generated rewrites.conf file due to how OpenLiteSpeed was configured.

The custom rewrites.conf file is located in:

```
/var/www/site.url/ols/rewrites.conf
```

### On GridPane OpenLiteSpeed .htaccess Changes do not Require a Restart

On regular OLS, once you’ve edited your .htaccess file, you will need to restart OpenLiteSpeed for those changes to take effect.

GridPane OpenLiteSpeed actively monitors .htaccess files for all of your sites using a file modification-based daemon and will take care of OLS reloads for you automatically.

If the custom rewrites.conf file has been modified, a specific OpenLiteSpeed command has to be executed in order for the changes to take effect (replace “site.url” with your domain name):

```
gpols site site.url
```

### Troubleshooting

If your mod_rewrite rules aren’t working as expected, you may find errors that explain why inside the error logs.

Run the following for the last 500 lines of the log file (replacing “site.url” with your domain name):

```
gpols log site.url
```

Available flags are -f to follow the log output in real-time, or -a for the access log. The command above defaults to error logs. Replace “site.url” with “httpd” for the server logs, which also uses the same flags.

```
gpols log httpd
```

 

## Restarting OLS with No Downtime

OpenLiteSpeed offers the ability to restart its service without any downtime. Downtime is minimal either way, but it’s a nice touch.

As mentioned above, if you’re making changes to .htaccess, these won’t automatically take place on OpenLiteSpeed like they would on LiteSpeed Enterprise. There are pros and cons here – the con being the minor inconvenience, the pro being that your clients can’t restart the service over and over again by playing developer.

### Restarting on the Command Line

The command below will generate a site’s vhconf, generate server conf, and then finally restart the OpenLiteSpeed service (replace “site.url” with your domain name:

```
gpols site site.url
```

To generate server conf only and restart service:

```
gpols httpd
```

To restart OpenLiteSpeed using systemctl run:

```
systemctl restart lsws
```

OR hard restart with this command:

```
/usr/local/lsws/bin/lswsctrl restart
```

### Restarting via Monit

The easiest option is to head to your Servers page inside your GridPane dashboard, and open up Monit for your server:

Here you can stop, start, reload/restart any of your services. Click on openlitespeed located under Process as highlighted here:

Scroll to the bottom of the OLS page and click the Restart Service button:

 

## Caching

OpenLiteSpeed of course comes with the excellent caching options that LiteSpeed is famous for. New WordPress websites created on OLS servers come with the LiteSpeed Cache plugin pre-installed.

OLS servers also offer Redis Object caching, just like Nginx servers, and you can toggle page caching ON and OFF directly inside your websites customizer on the Sites page in your GridPane account.

These changes will then be reflected directly inside your WordPress website in the LS Cache plugin settings.

In the near future we will release a detailed article covering the settings inside the LiteSpeed Cache plugin.

 

## PHP Workers

LiteSpeed and OpenLiteSpeed run PHP LiteSpeed SAPI, which is a custom version of PHP specific to LiteSpeed Web Servers.

Just like Nginx, OpenLiteSpeed offers a number of different PHP process modes via PHP LSAPI: ProcessGroup mode, Daemon mode, and Worker mode.

We use the recommended settings as outlined by LiteSpeed as the out-of-the-box defaults. Unless you have a very specific use case for them, we recommend you use the ProcessGroup mode for all of your websites as opposed to the Worker mode. ProcessGroup mode also takes advantage of opcode caching.

Daemon mode does not allow the use of custom per-user php.ini, and so individual websites can’t be customized. This is a common choice for shared hosting environments, but due to its customization limitations, this option isn’t available on GridPane.

To learn more about PHP workers and how they impact your website’s performance, please check out our detailed guide here:

PHP Workers and WordPress: A Guide for Better Performance

Skip to part 4 if you want to dig into worker type specifics.

 

## Security Hardening

GridPane includes a lot of options to help secure your websites. These are available on both our OpenLiteSpeed stack and our Nginx stack.

### WordPress Hardening

You can learn about all of the website hardening options available here:

WordPress Website Hardening for Nginx and OpenLiteSpeed

### Web Application Firewalls (WAFs)

OpenLiteSpeed doesn’t include the 6G WAF, as the more up-to-date version is available to all Developer accounts and above. Learn all about 7G here:

Using the GridPane 7G Web Application Firewall

The ModSecurity WAF is also available via GP-CLI, and will be available inside the Security tab as a toggle in the near future. The commands for both Nginx and OpenLiteSpeed servers are the same, and you can learn more about ModSecurity here:

Using the GridPane ModSec Web Application Firewall

### Fail2Ban

Our Fail2Ban CLI for protecting /wp-login.php and /xmlrpc.php, and our integration with the WPFail2Ban plugin are both available, again with the same commands. We highly recommend that you use the plugin integration for your websites. Learn more here:

Configuring Fail2Ban to Prevent Brute Force Attacks

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

