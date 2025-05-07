# I got an email from Let’s Encrypt about my SSL expiring, what do I do? | GridPane

# I got an email from Let’s Encrypt about my SSL expiring, what do I do?

 

4 min readLet’s Encrypt sends notifications about your SSL’s and it can be an email like the following:

————

Hello,

Your certificate (or certificates) for the names listed below will expire in 19 days (on 01 Apr 20 16:00 +0000). Please make sure to renew your certificate before then, or visitors to your website will encounter errors.

We recommend renewing certificates automatically when they have a third of their
total lifetime left. For Let’s Encrypt’s current 90-day certificates, that means
renewing 30 days before expiration. See https://letsencrypt.org/docs/integration-guide/ for details.

abcdefghstat.domain.com

For any questions or support, please visit https://community.letsencrypt.org/. Unfortunately, we can’t provide support by email.

————

If you received an email like this, chances are it’s because the site or server where this SSL was issued is no longer online. For example, if you add a site on server A, get an SSL, then move the site to server B, and get a new SSL (if the old one hasn’t been migrated), you’ll get an email about the certificate that was on server A.

If you received a similar message to this: Let’s Encrypt certificate expiration notice for domain “wehcjiojifstat.gridpanevps.com” then this can safely be ignored. This is an SSL for either Monit or PHPMyAdmin on a server that likely no longer exists.

### Check Your Websites SSL

If the email was for one of your websites, one easy way to check is to pull up the domain in question and confirm the dates match:

If the dates don’t match, it means the SSL currently on your site is not the one that is actually expiring. You can probably disregard it.

If this isn’t the case and the website is still live on your server, continue below, and if you’re ever in doubt, contact support, and we would be happy to check.

## Checking the Certbot Monitoring Log

To view the specific error that’s prevent your SSL from renewing, you can check out your servers certbot.monitoring.log.

To do this, you first need to SSH into your server. Please see the following articles to get started:

Generate your SSH Key:

Generate SSH Key on Mac

Generate SSH Key on Windows with Putty

Generate SSH Key on Windows with Windows Subsystem for Linux

Generate SSH Key on Windows with Windows CMD/PowerShell

Add your SSH Key to GridPane:

Add default SSH Keys

Add/Remove an SSH Key to/from an Active GridPane Server

Connect to your server:

Connect to a GridPane server by SSH as Root user.

Once logged in run:

```
cd /opt/gridpane/
```

Followed by

```
cat certbot.monitoring.log
```

Here you’ll see a rundown of the SSL’s that have failed to renew as well as their cause.

Usually, these logs will help you identify the issue immediately, and the most common errors include DNS records not existing or the A Name record is pointing to an IP address other than the servers.

For example:

```
Errors: 
IMPORTANT NOTES:
The following errors were reported by the server:
Domain: domain.com Type: unauthorized Detail: Invalid response from http://domain.com/.well-known/acme-challenge/lLTYAuvHR3AXxU_yadewfgwergWIOEfeWFnkJFRj [15.15.37.164]: 404
Domain: www.domain.com Type: unauthorized Detail: Invalid response from http://www.domain.com/.well-known/acme-challenge/NOaYboK-1mKaW7ohSXZpWF-TuXFad3ZergQEheSFFVHrgefgJPHD [66.70.196.106]: 404
To fix these errors, please make sure that your domain name was entered correctly and the DNS A/AAAA record(s) for that domain contain(s) the right IP address.
```

These errors can sometimes be caused by services like Cloudflare who hide the IP address of your origin server.

## Cloudflare

If your domain is running on Cloudflare’s proxy servers and you’ve used the webroot method to provision your SSL (your website isn’t using Cloudflare/DNSME API integration), then the cause may be that Let’s Encrypt isn’t able to verify your server IP.

Cloudflare doesn’t always cause Let’s Encrypt renewal failures, but it’s possible this could be the underlying cause if Let’s Encrypt can’t verify your DNS.

If you’re unsure, you can quickly check if the website in question is on Cloudflare by entering the domain here:

https://www.ultratools.com/tools/ipWhoisLookup

If it is on Cloudflare, then turn the clouds from orange to grey inside the DNS tab in your Cloudflare account, and then try running on your server:

```
certbot-auto renew --dry-run
```

If all goes well, you can then run:

```
certbot-auto renew
```

Or shoot us a message on support and we’ll take a look into it for you.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

