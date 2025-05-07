# Monit SSL Renewal Failure Notification in the Dashboard or Slack | GridPane

# Monit SSL Renewal Failure Notification in the Dashboard or Slack

 

4 min read 

### Table of Contents

 

## Introduction

Monit checks your SSL renewal logs once per day and if a renewal failure has occurred it will trigger a notification in your dashboard and send a notification to Slack (if you have Slack notifications enabled).

Often a renewal failure is one-off event. This is easy to check and confirm, and if it is a one-off failure, the notice inside Monit will disappear the next time it checks the log.

 

## The SSL Monitoring Logs

The method you used to provision your SSL will determine which log is monitoring your renewals. If you used a DNS API integration (via Cloudflare or DNS Made Easy) to provision your SSL, the Acme Monitoring Log will contain the details you need. For regular, webroot SSL certificates, the Certbot Monitoring Log will be where you need to check.

Both of these logs can be found inside your server customizer.

Head over to the Servers page inside your account and click on the name of the server you wish to check. This will open up the customizer:

The log is located inside the Logs tab.

Click the icon to open up the log. Logs are for 24 hours and at the bottom you can also navigate between previous days if you wish to do so.

On the server the logs are located in the following locations:

The Certbot Monitoring Log is here:

```
/opt/gridpane/certbot.monitoring.log
```

The Acme Monitoring Log is here:

```
/opt/gridpane/acme.monitoring.log
```

You can learn more about site and server logs and where they live in this article:

GridPane Logs – How to Find Them and When to Use Them

 

## Reviewing the Logs

If reviewing the log in your browser, once the log is open you can use CTRL+F to open up a search and type the word “Error“. This will make it easy to locate any failures without scanning the entire log line by line.

If no failures exist today, then this was likely a one off event and Monit will report all is well the next time it checks the log.

### Example Renewal Failure 1

A common error you may see is this:

```
1 renew failure(s), 0 parse failure(s)

IMPORTANT NOTES:
 - The following errors were reported by the server:
   Domain: www.yourdomain.com
   Type:   dns
   Detail: DNS problem: NXDOMAIN looking up A for
   www.yourdomain.com - check that a DNS record exists for this domain
```

What this means is that when you provisioned this SSL certificate, you were given a certificate for both domain.com and www.domain.com because that is what certbot saw at the time but then the www record was removed. An SSL must be renewed with the same records as it was provisioned with, or it throws an error.

Solution: Create a DNS record for www

You can learn how to set up your DNS records here: Setting DNS Records

If for some reason you do not want to have www on your certificate, you can also remove the existing SSL and provision another one.

### Example Renewal Failure 2

Another common error is:

```
Errors: 
IMPORTANT NOTES:
The following errors were reported by the server:
Domain: domain.com Type: unauthorized Detail: Invalid response from http://domain.com/.well-known/acme-challenge/lLTYAuvHR3AXxU_yadewfgwergWIOEfeWFnkJFRj [15.15.37.164]: 404
Domain: www.domain.com Type: unauthorized Detail: Invalid response from http://www.domain.com/.well-known/acme-challenge/NOaYboK-1mKaW7ohSXZpWF-TuXFad3ZergQEheSFFVHrgefgJPHD [66.70.196.106]: 404
To fix these errors, please make sure that your domain name was entered correctly and the DNS A/AAAA record(s) for that domain contain(s) the right IP address.
```

These errors can sometimes be caused by services like Cloudflare who hide the IP address of your origin server.

Here you would need to check your DNS records, and potentially turn off your CDN or Cloudflare proxy to run the renewal.

 

## What Causes SSL Renewal Failures?

Failures can occur for a variety of reasons.

If using the webroot method, these include:

For DNS API certificates, issues include:

It’s also possible that Let’s Encrypt was under maintenance or having an issue at the time the renewal took place, which means it failed even though everything was set correctly for your domain.

More often than not the reason for the failure will be obvious inside the log, and you can then fix the issue based on what Let’s Encrypt added under “IMPORTANT NOTES”.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

