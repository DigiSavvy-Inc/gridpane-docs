# GridPane Logs - How to Find Them and When to Use Them | GridPane

# GridPane Logs – How to Find Them and When to Use Them

 

16 min read 

## Introduction

Knowing where your logs are and what they keep track of is an important part of managing your WordPress web hosting business. In this article, we’ll take a look at where you can go to view your server logs, and when you might want to check them. Some, for example the SSL log and Nginx error logs, are particularly important and you’ll refer to some of these logs a lot more than others.

There’s also the “Server Health Check” function and log which we’ll briefly cover here as well, and there will be a link to a more in-depth article. This is a pretty awesome feature that’s custom-built for GridPane, and it’s something you’ll want to check out and make use of somewhat regularly.

You can view almost all of your logs directly within your dashboard. The only current exceptions are the Web Application Firewall logs which are detailed in part 5.

 

## GridPane Server Logs

These logs contain information relating to your server as a whole.

You can view your server logs by heading to the Servers page inside your GridPane account, and clicking on the name of your server.

This will open up the server customizer modal as shown in the image below, and the logs are contained in the Logs tab. To open up a log, simply click on the icon next to the log name in the view column.

 

### Auth Log

The auth log is responsible for logging all authentication-related events. You can use this log to view failed login attempts, identify brute force attacks, or anything that related to suspicious authentication attempts.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/php/auth.log
```

 

### Fail2Ban Log

The Fail2Ban log is responsible for logging all Fail2Ban related events. Here you can check on IPs that have been banned/unbanned. You’ll notice a lot of “Found”, which means these IPs are logged, but not exceeding the thresholds for bad behaviour that result in an actual ban.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/fail2ban.log
```

 

### GP Clone Log

The GridPane Clone Log keeps track of all website cloning events. If you clone any of the websites on your server, it will be logged here. If you experienced a cloning failure, you can check this log for details of what may have gone wrong.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/opt/gridpane/gpclone.log
```

 

### Health Check Log

The Health Check Log will be created when you run your first server health check. It will perform a series of checks on your server and then give it a score. You can use the information in this log to help determine when it’s time to scale up, free up disk space, and spot/diagnose other potential issues that could cause or be causing your websites issues. It can take several minutes to complete, and will then display the results directly in the log.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/health-check.log
```

 

### Monit Log

The Monit Log keeps track of events related to the services it monitors. Here you’ll see when Monit detects errors and restarts services them to keep your server fully operational. If you’re experiencing issues specific to a service (Nginx, MySQL, PHP, Redis), you’ll be able to get a good look at what’s going on inside your server with this log.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/monit.log
```

 

### UFW Log

UFW stands for Uncomplicated Firewall. It’s a program for managing a netfilter firewall. While “uncomplicated” is true in it’s setup, reading the logs is actually a little complicated. For a thorough walkthrough on how to make sense of the events in this log, this answer on AskUbuntu gives a step by step explanation.

It’s unlikely you will ever need to check this log, however, we include it here to be thorough and make access to it easy for veteran Sysadmins.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/ufw_log
```

 

### Certbot Monitoring Log

The Certbot Monitoring Log keeps track of SSL certificate renewals for SSL’s that were provisioned using the webroot method – the website is not using a DNS API integration, and was provisioned after the DNS records were changed. If you’ve had a notice about an SSL certificate failing to renew, this log will provide the answers as to why it failed.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/opt/gridpane/certbot.monitoring.log
```

 

### Acme Monitoring Log

The Acme Monitoring Log keeps track of SSL certificate renewals for SSL’s that were provisioned using the DNS API Full method, or API Challenge method. It’s extremely rare that SSL’s provisioned this way later fail, but should you have any trouble this log will provide insight into what’s happened.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/opt/gridpane/acme.monitoring.log
```

 

### MySQL Error Log

The MySQL Error Log keeps track of startup and shutdown times, and any errors that may occur during this process. They also log if any tables need to be checked/repaired. If you’re experiencing any database related issues on any of your sites, you may find helpful info in this log.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/mysql/error.log
```

 

### PHP 7.4 FPM Log (Nginx)

The PHP 7.4 FPM Log keeps track of PHP 7.4 startup and restart events.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/php/7.4/fpm.log
```

 

### PHP 8.0 FPM Log (Nginx)

The PHP 8.0 FPM Log keeps track of PHP 8.0 startup and restarts events.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/php/8.0/fpm.log
```

 

### PHP 8.1 FPM Log (Nginx)

The PHP 8.1 FPM Log keeps track of PHP 8.1 startup and restarts events.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/php/8.1/fpm.log
```

 

### PHP 8.2 FPM Log (Nginx)

The PHP 8.2 FPM Log keeps track of PHP 8.2 startup and restarts events.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/php/8.2/fpm.log
```

 

### PHP 8.3 FPM Log (Nginx)

The PHP 8.3 FPM Log keeps track of PHP 8.3 startup and restarts events.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/php/8.3/fpm.log
```

 

### Redis Log

The Redis Log keeps track of all Redis related events being saved on your server. This includes shutdowns, restarts, and memory usage.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/redis/redis-server.log
```

 

### Syslog

Syslog can actually refer to a few different things – the syslog service, the syslog protocol, and/or a syslog message. For our purposes here, this log is a system related events log.

If you’d like to dig deeper into the Linux Syslog, this article over at Loggly.com is a good place to start:

https://www.loggly.com/ultimate-guide/linux-logging-basics/

It’s unlikely you will ever need to check this log, however, we include it here to be thorough and make access to it easy for veteran Sysadmins.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/syslog
```

 

### Automated Backups Monitoring Log

The GridPane Backups log keeps track of all the website backups that take place on your server. If you want to check when specific websites are being backed up, they will be detailed in this log.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/opt/gridpane/backups.monitoring.log
```

 

### OpenLiteSpeed STDERR.log (Not Available in UI)

The stderr.log is only accessible via the command line at this time. This log is usually the most helpful when determining why PHP is throwing 503 errors.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/usr/local/lsws/logs/stderr.log
```

 

### OpenLiteSpeed Web Server Error.log (Not Available in UI)

The web server error log may provide helpful hints as to whether the web server caused PHP to fail.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/usr/local/lsws/logs/error.log
```

As an additional note, the following can be useful for diagnosing 503 errors. However, most of the time, the error log doesn’t give you the reason why the 503 error happened. It only shows you when it happened and with which domain it happened.

```
grep oops /usr/local/lsws/logs/error.log
```

 

### Git Error Log

The Git Error Log records any Git specific errors that may have taken place.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/opt/gridpane/git.error.log
```

 

## MySQL Slow Log

The MySQL slow query log is where the MySQL database server will log all queries that exceed the time (in seconds) that you specify. This can be particularly helpful on database-intensive websites, such as WooCommerce stores, to help identify long-running processes, and fix them for better performance. You can learn more about using the MySQL Slow Log here:

Using the MySQL Slow Log

### View the Log

On Developer and Agency accounts, the MySQL slow log can be activated and viewed within the UI. It’s located within the Server customizer inside the MySQL tab:

Click the View MySQL Slow Query Log button to display the log.

### Slow Log Server Location

The log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/mysql/error.log
```

 

## Website Specific Logs

Your website specific logs are going to be the first place you head to in many instances if/when you need to start diagnosing any issues that occur. The SSL provision log and the Nginx site error log in particular will be of great help in diagnosing SSL and performance related issues. Our support team may also ask you to provide us with information from these logs if you reach out to us for assistance.

You can view your website specific logs heading to the Sites page inside your GridPane account, and clicking on the name of your website.

This will open up the website configuration/customizer modal, and the logs are contained in the Logs tab.

 

 

### Log Location Note

Below you'll see the locations for each log contain "site.url" in the file paths. To view your website logs, you will need to replace this with your domain name. For example:

/var/www/site.url/logs/debug.log

Would look like the following, just with your own domain: 
/var/www/gridpane.com/logs/debug.log

### Secure WP Debug Log

If you’ve turned on WP Debug, all debug related events will be logged here. If you’d like to learn more about using WP Debug along with the Query Monitor plugin (which will be auto-installed on your website when you flip the Enable Secure WP Debug toggle to ON), check out this article.

Be sure to always turn debug off once you’ve finished using it.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/debug.log
```

 

### GridPane General Log

The general logs keep track of the changes made to your website in the site customizer. You can view changes that have been made to your site in this log.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/gridpane-general.log
```

 

### Domains Log

The Domains Log keeps track of events related to domain addons (alias and redirects), and primary domain swaps. If you need to retrace the history of a website when it comes to the domains attached to it, you’ll be able to find date and times for all events in this log.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/domains.log
```

 

### Manual Backups Log

The Manual Backyups Log keeps track of all the manual backups that you take for your individual sites. If a backup ever fails to complete, the reason will be detailed in this log.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/manual-backups.log
```

 

### Single Sign-On (SSO) Log

The SSO log tracks Single Sign-On events, including the magic link associated with each login. If you’ve experienced trouble with SSO, you’ll be able to check this log for more information, and also find the link that’s been created. These links expire after 15 minutes or immediately after they have been used. You may still be able to SSO into your sites by copying and pasting these links if they aren’t opening in a new window for you.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/sso.log
```

 

### SSL Provision Log

The SSL provision log keeps track of all SSL provisioning attempts, and includes detailed information about each process. This is one of the most commonly used logs, and if you experience an SSL failure, this log will be the first place you should check. All failed SSL attempts include a detailed reason as to why they failed, and you will need to use this information to make the necessary corrections before attempting to provision another SSL certificate.

The most common reason will be that your DNS records are not correct. Please see this article for further diagnosing SSL related issues:

Diagnosing and Fixing SSL Certificate Issues

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/ssl-provision.log
```

 

### Staging Push Log

The Staging Push Log records all instances of any Live -> Staging, or Staging -> Live pushes. If you experienced a staging push fail, this log will help identify the reason for the failure.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/staging.log
```

 

### Nginx Site Access Log

The Nginx Site Access Log records the IP addresses of those that visit your websites, what they do, what browser they use, the names of the bots that crawl your site, and more.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/nginx/site.url.access.log
```

 

### OpenLiteSpeed Site Access Log

Same as Nginx above but for OLS servers.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/ols/site.url.access.log
```

 

### Nginx Site Error Log

The Nginx Site Error Log records all general website errors. This is one of the logs you should familiarise yourself with as it will help identify all kinds of potential issues like plugin conflicts, PHP errors, timeouts, and more, that can help you pinpoint the source of performance-related issues. If you’re experiencing any kind of strange behaviour on one of your websites, this log should be the first place you check, and from there you can begin digging deeper into the issue.

ModSecurity Firewall events are also logged here.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/nginx/site.url.error.log
```

 

### OpenLiteSpeed Site Error Log

Same as Nginx above but for OLS servers.

ModSecurity Firewall events are also logged here.

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/ols/site.url.error.log
```

 

## PHP Slow Log

The PHP slow log, like the MySQL slow query log, is useful for diagnosing long-running processes that are having a negative effect on your website’s performance. Learn more here:

Using the PHP Slow Log

### View the PHP Slow Log

For Developer and Agency accounts, you can view the PHP Slow Log directly inside the UI. The PHP Slow log is located in the website configuration modal, inside the PHP tab:

Click the button next to “View Site PHP-FPM slowlog” to display the contents of the log.

### Server Location

The log name will vary depending on which version of PHP you’re using, but it will be located in /var/log. The log will be your websites name, followed by the PHP version without the “.” between the two numbers.

Here’s an example for PHP 7.3:

```
/var/log/site.url73.log.slow
```

 

## Web Application Firewall Logs

Firewalls can sometimes have unexpected results, such as blocking plugins or external service that you’re trying to use. To begin diagnosing these issues, we have detailed examples in each of our Firewall Knowledge Base articles.

These logs each record all firewall related events for your individual websites, and you can use them to diagnose the specific rules that are being broken by the plugin/service you’re trying to use.

Below we’ll quickly cover where you can find WAF logs for your individual websites.

 

### 6G WAF

The log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/6g.log
```

KB Article: Using the GridPane 6G Web Application Firewall

 

### 7G WAF

The log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/www/site.url/logs/7g.log
```

Full KB Article: Using the GridPane 7G Web Application Firewall

 

### ModSecurity WAF

ModSecurity events are logged in the Nginx Site Error Log, detailed in the Website Specific Logs section above.

```
/var/log/nginx/site.url.error.log
```

Full KB Article: Using the GridPane ModSec Web Application Firewall

 

## Accessing Your Logs Directly and/or Downloading Your Logs

If you’d like to download a copy of these to your computer you can do so by accessing your server over SFTP as the Root user. Here’s our KB on how to get started:

Connect to a GridPane Server by SFTP as Root user

If you’d like to view them directly on your server, you can see the following guides to get started setting up your SSH Keys, and connecting over SSH:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

Once connected you can use the cat command, followed by the log file paths detailed throughout this article, for example:

```
cat /path/to/example.log
```

Or you can view them in real time with the tail -f command:

```
tail -f /path/to/example.log
```

To exit from tail -f hit CTRL+C.

For a real world example, to view the MySQL Slow Log, you can use the following command:

```
cat /var/log/mysql/slow.log
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

