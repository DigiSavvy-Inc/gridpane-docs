# Diagnosing and Fixing SSL Certificate Issues | GridPane

# Diagnosing and Fixing SSL Certificate Issues

 

21 min read 

## Introduction

In this article, we’ll take a look at all of the SSL issues you may see when working with your websites on GridPane. With the exception of Let’s Encrypt conducting maintenance, these are all easy to diagnose and fix, and easily preventable once you understand the reasons behind them.

This includes everything from provisioning a new SSL certificate, failed SSL renewals, SSL errors in the browser, unexpected redirects, and our internal locks that are in place to prevent you from getting rate limited.

### Table of Contents

###### Part 1: Information and Initial Diagnosis

###### Part 2. Specific SSL Issues

 

Part 1: Information and Initial Diagnosis

 

## DNS API vs Webroot Verification

GridPane allows you to provision free A+ grade SSL certificates via Let’s Encrypt.

It’s important to note here that SSL certificate provisioning works differently if you’re using either our DNS Made Easy or Cloudflare DNS API integrations. In these cases, you do NOT need to point your DNS A record to your website’s IP address to provision an SSL.

If you’re not using a DNS API integration then your SSL will be provisioned using the webroot method. This requires that your DNS be in place and pointing to your website’s server IP address for it to be successful (#2 on the list below).

You can learn about the different SSL provisioning methods in the links below:

Provisioning SSL Certificates

 

## Diagnosing SSL Failures

When provisioning an SSL certificate, Let’s Encrypt GridPane will log the entire process from start to finish in your website’s SSL log.

It will also make a clear note in this log if your provision attempt fails, detailing the exact reason Let’s Encrypt has given for this failure.

This should be your first port of call when you experience an SSL provisioning failure. It’s exactly what we’ll ask if you for if reach out to support, and this is how we begin when looking at SSL provisioning failures.

### Step 1. Open your sites configuration modal

To view your log, head over to your Sites page inside your account:

Click on the website you’re trying to provision an SSL for, and then click on the Logs tab. Here you can open up your SSL log:

### Step 2. Open up the log and check the error notes

The error notice will be close to the bottom, so scroll down and find the IMPORTANT NOTES:

As you can see, in this case, I haven’t set the DNS records to point to the IP address. The solution is to set them, wait for them to go live worldwide, and then try again.

Your error may be different, and if you’re not sure how to fix it, you can reach out to us on support, and we can help guide you through this.

 

 

### IMPORTANT

The exception to the rule with Let's Encrypt returning the reason they didn't issue the SSL is that maintenance at Let's Encrypt is currently ongoing and some of their services are down. In this case, it's possible that a tangible reason may not be given. See below for more details.

## Maintenance at Let’s Encrypt, DNSME, or Cloudflare

It’s possible to set everything up correctly and still experience a provisioning issue or a renewal failure due to a provider outage or provider maintenance.

An outage or maintenance at Let’s Encrypt could affect your ability to provision an SSL or certbot’s ability to renew an SSL. If there’s an issue at Let’s Encrypt, then they will need to resolve this at their end before begins working again but don’t hesitate to reach out to support to confirm, as this is extremely rare.

An outage or maintenance at Cloudflare or DNS Made Easy could prevent you from being able to provision an SSL via the DNS API method. If this is the case, then you could attempt to provision an SSL using webroot verification by setting your DNS to point to your website.

You can check on the status of each of these providers via the links below:

 

## DNS Isn’t Pointing to Your Servers IP Address

If you aren’t using one of our DNS API integrations, then your SSL will be provisioned using the webroot method. This is where Let’s Encrypt checks your website against the domain’s live DNS records to make sure you’re website’s server IP and DNS records set IP match up.

If they match up correctly, the SSL will proceed. If you haven’t set your DNS yet and you’re trying to provision an SSL, it will fail. The solution is to set your DNS records, and once they go live worldwide, try again.

You can check the live status of your domain’s DNS with the following free tool:

https://dnschecker.org/#A

Before you toggle on your SSL again, please check and make sure your DNS is pointing to the correct IP address at all locations worldwide. Nowadays, this is very quick for most providers (5 minutes or less), but there are still some that can take some time – even up to 24 hours.

 

Part 2: Specific SSL Issues

 

## GridPane SSL Locks

We’ve implemented a system that will lock and prevent SSL provisioning attempts from proceeding once you experience provisioning failures 3 times in a row.

Removing the lock is simple, but we put this in place to ensure our users can’t hit the Let’s Encrypt rate limit by continually re-attempting again and again until they hit their limit and lock you out.

If you’re experiencing an SSL Lock, you can follow this guide to remove your lock:

GridPane SSL Locks and Let’s Encrypt Rate Limiting

Please be sure to follow the steps in #3 above to ensure that you don’t get yourself rate limited by Let’s Encrypt – more information on their rate limiting below.

 

## Let’s Encrypt Rate Limiting

Let’s Encrypt use rate-limiting to prevent abuse of their [excellent] free service.

You get 5 attempts to provision an SSL (which should be plenty). If you fail 5 times in a row, you’ll be blocked from re-attempting for 7 days.

We don’t want that to happen, and as long as you are following our documentation, it should never happen to you.

You can learn more about Let’s Encrypt rate limits here: https://letsencrypt.org/docs/rate-limits/

### Workarounds

If you do get rate limited, there’s, unfortunately, nothing that our support team can do to get this lifted before that 7 days is up. However, there are some workarounds you can employ.

These are:

Full details on the above 3 options can be found in this article:

Workarounds: What to Do if You’ve Been Rate Limited by Let’s Encrypt

 

## A Wildcard SSL Won’t Provision

If you’re having trouble with a Wildcard SSL, be sure to carefully check your work with our guides:

Make sure Wildcard is toggled on, and that you have your domain set up with either the DNS Made Easy or Cloudflare DNS API integration. These are necessary as Let’s Encrypt does not allow the provisioning of a Wildcard SSL using the webroot method.

 

## You have an SSL Certificate but no Padlock Icon

The Problem: You have your SSL certificate, but when you go to your website, you’re not seeing the padlock icon next to your domain name in the address bar.

The reason for this is that you have mixed content on your site, meaning some assets are served correctly over HTTPS, but others are loading over HTTP.

A great resource for determining why this is happening is:

https://www.whynopadlock.com/

If WhyNoPadlock doesn’t pick up on the error, then it’s likely to be a slow-loading asset. In that case, you can also use Google Console:

The solution to this issue is to change any links loading over HTTP to HTTPS. You can usually do this in bulk with a find-and-replace plugin such as Velvet Blues. Check out this article for more information:

How to Search and Replace in a WordPress Database

 

## SSL Renewal Warnings and Failures

If you have an SSL that fails to renew, Let’s Encrypt will send you an email to let you know.

Usually, these occur when you’ve moved this particular website to a different server, and certbot on the old server is trying to run the SSL renewal but failing because the site is located at a new IP address.

To check, you can click on the padlock icon next to your domain name in the address bar, and check the date.

Do the dates match up? If not, then you can safely ignore this message.

For more details on checking this directly on your server, please check out the following article:

Why am I not seeing a padlock on my site?

If you received a similar message to this: Let’s Encrypt certificate expiration notice for domain “wehcjiojifstat.gridpanevps.com” then this can also be safely be ignored. This is an SSL for either Monit or PHPMyAdmin on a server that likely no longer exists.

### Legitimate Renewal Failures

More often than not, this is nothing to worry about, however, there is an issue that can occur on subdomains when Cloudflare proxy is enabled. It’s the same error detailed in issue number 10 of this article: ERR_SSL_VERSION_OR_CIPHER_MISMATCH.

Running a manual renewal attempt (the little refresh icon next to your SSL toggle) will show the following error in the log:

 

```
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/subdomain.example.com.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Simulating renewal of an existing certificate for subdomain.example.com and www.subdomain.example.com

Certbot failed to authenticate some domains (authenticator: webroot). The Certificate Authority reported these problems:
  Domain: www.subdomain.example.com
  Type:   tls
  Detail: Fetching https://www.subdomain.example.com/.well-known/acme-challenge/735Ok_twivVMMIXmUDheD3SKGgeJFKDOSF0932sdsfeRjJI: remote error: tls: handshake failure

Hint: The Certificate Authority failed to download the temporary challenge files created by Certbot. Ensure that the listed domains serve their content from the provided --webroot-path/-w and that files created there can be downloaded from the internet.
```

Note this is only for the www version of the website, but it still prevents the renewal from going through.

If you visit the www version of your website, you will be able to confirm the issue in number 10 is the root cause. Toggle off the Cloudflare proxy and wait a few minutes for the DNS to change worldwide and for the site to work correctly again over www. At this point, run the renewal attempt again, and it will go through correctly.

 

## Too Many Redirects Error

This comes up frequently with new users who use Cloudflare. This is caused when the SSL setting within your Cloudflare is set to “Flexible” instead of either “Full” or “Full Strict“.

To fix this, simply ensure that it’s not set to Flexible – typically, we recommend Full Strict as it’s better for accurately diagnosing other potential SSL issues in the unlikely event that they should ever occur.

If it’s not Cloudflare related, then there’s something on your WordPress installation that’s causing a redirect issue. You can double-check the issue with Redirect Checker, and it’s likely to be plugin related.

 

## SSL Error Only on “www” Version of Site

When provisioning an SSL using the webroot method (which relies on your DNS records pointing to your server in advance), Let’s Encrypt will try to verify both your root domain and the www version of your website.

If for any reason, it can’t verify the www version of your site, it will attempt to continue and only provision an SSL for the root.

This will also come through in your notifications if you’re watching them come through.

### Check Your SSL Log

If you check the website SSL log, you will see something similar to the log below:

 

```
-------------------------------------------------------------------
Testing example.com.site DNS records before attempting to provision SSL...
example.com.site IP: 
199.199.199.19
www.example.com.site IP/CNAME: 
Not resolving
-------------------------------------------------------------------
Proceeding to do a Lets encrypt Dry Run for both: 
example.com.site, www.example.com.site
-------------------------------------------------------------------
Account registered.
Simulating a certificate request for example.com.site and www.example.com.site

Certbot failed to authenticate some domains (authenticator: webroot). The Certificate Authority reported these problems:
  Domain: www.example.com.site
  Type:   dns
  Detail: DNS problem: NXDOMAIN looking up A for www.example.com.site - check that a DNS record exists for this domain; DNS problem: NXDOMAIN looking up AAAA for www.example.com.site - check that a DNS record exists for this domain

Hint: The Certificate Authority failed to download the temporary challenge files created by Certbot. Ensure that the listed domains serve their content from the provided --webroot-path/-w and that files created there can be downloaded from the internet.

Saving debug log to /var/log/letsencrypt/letsencrypt.log
Some challenges have failed.
Ask for help or search for solutions at https://community.letsencrypt.org. See the logfile /var/log/letsencrypt/letsencrypt.log or re-run Certbot with -v for more details.
-------------------------------------------------------------------
Dry Run failed.
-------------------------------------------------------------------
Proceeding to do a Lets encrypt Dry Run for:
example.com.site
Simulating a certificate request for example.com.site
The dry run was successful.
```

### Fixing the Issue

To get the SSL working for the www version of your website, you will first need to make your www CNAME or A record is correct worldwide. We recommend this website:

https://dnschecker.org/

Next, toggle the SSL to OFF in your domains tab, and then toggle it back ON.

NOTE: The refresh icon will not fix this. It will simply try to renew the existing SSL, which doesn’t include the www version.

 

## ERR_SSL_VERSION_OR_CIPHER_MISMATCH / SSL_ERROR_NO_CYPHER_OVERLAP

These rather obscure error codes can show themselves when using sub.sub.domains with Cloudflare’s services, and by this, I mean on domains where the “orange clouds” are active, and you’re using services such as their CDN, Firewall rules, etc.

It is a possibility that you might run into this error when using Cloudflare on the staging sites of subdomains.

These two errors are named slightly differently depending on the browser you’re trying to visit the website with.

In Chrome, Microsoft Edge, and other Chromium-based browsers, the error is: ERR_SSL_VERSION_OR_CIPHER_MISMATCH

In Firefox, the error is: SSL_ERROR_NO_CYPHER_OVERLAP

In Safari, it might simply say: “Safari cannot open the page because it could not establish a secure connection to the server”.

### The Problem

Two-level deep sub-domains are not supported by Cloudflare for SSL.

For example, to grab the two screenshots for this article, I set up the website “cfssltest.waas.monster“. The primary domain is, of course, waas.monster, and the website I’ve created is a subdomain. If I activate an SSL on this, Cloudflare will have no issues whatsoever.

However, I also have the staging site for this website which is: “staging.cfssltest.waas.monster“. Cloudflare does not support SSL at this level, and it will result in the errors noted above when you try and visit your website.

### The Solution

Inside your Cloudflare account, click on the domain you’re having trouble with, and then click through to its DNS settings page.

Here you want to change the orange cloud to a grey cloud:

Once that change has been made, Cloudflare has been switched to DNS-only mode, and their services will no longer be active on the site. This will fix the SSL cipher issue.

 

## Forced HTTP > HTTPS Prior to SSL

If you’re using the webroot method to provision your SSL and everything is set up correctly, this can be a confusing issue to troubleshoot. Everything appears to be in order (your DNS records are all correct, and you’ve confirmed with https://dnschecker.org/#A, but Let’s Encrypt is continually failing the dry runs.

### The Problem

In your website’s SSL log, if you can see in the line that begins with “Detail: Fetching https://....” then Let’s Encrypt will be unable to verify your domain, as it can’t access your site over HTTPS without a valid SSL certificate already in place.

If it ends with “Connection reset by peer“, then you likely have a custom Nginx level redirect that is forcing your website to be served over HTTPS.

The whole block in the log will look like this:

 

```
-------------------------------------------------------------------
Proceeding to do a Lets encrypt Dry Run for both: 
example.com, www.example.com
-------------------------------------------------------------------
Simulating a certificate request for example.com and www.example.com

Certbot failed to authenticate some domains (authenticator: webroot). The Certificate Authority reported these problems:
  Domain: example.com
  Type:   connection
  Detail: Fetching https://example.com/.well-known/acme-challenge/Q9F3aU3daEH4iWqQWVTdctaVHnH_q2WPNQSS6FGQp4s: Connection reset by peer

  Domain: www.example.com
  Type:   connection
  Detail: Fetching https://www.example.com/.well-known/acme-challenge/LwkXA42dUUTObUYfxJIXUy1FjA67eD2oGD_85KbuGfI: Connection reset by peer

Hint: The Certificate Authority failed to download the temporary challenge files created by Certbot. Ensure that the listed domains serve their content from the provided --webroot-path/-w and that files created there can be downloaded from the internet.
```

### The Solution

Fix the forced HTTPS redirect.

If using Cloudflare, turn off the proxy and wait for your DNS records to resolve to your server.

### The Solution for Nginx Configs

Connect to your server and head to your website’s Nginx folder:

```
cd /var/www/site.url/nginx
```

Check any configuration files that you’ve added for forced HTTP > HTTPS redirects and remove those redirects.

Save the file, and check your Nginx  syntax with:

```
nginx -t
```

If all is OK, then reload Nginx with:

```
gp ngx reload
```

### An Example

An example where we’ve seen is the Flying Press plugin Nginx configuration which contains:

```
Force HTTPS
if ($scheme = http) {
return 301 https://$http_host$request_uri;
}
```

This is unnecessary on GridPane (and in general). Our configs reroute to HTTPS automatically when an SSL is enabled, and so this doesn’t add anything necessary or beneficial. Instead, it actually creates the possibility for problems like these.

With no SSL, your website is set up to only be served over HTTP. This redirect, however, is forcing all requests to HTTPS, including those before the .well-known location, and so Let’s Encrypt is being forced to redirect over HTTPS when attempting to run its checks, and these ultimately fail, resulting in your SSL failures.

 

## Cloudflare 526 Error

526 is a Cloudflare-specific error that occurs when Cloudflare can’t validate an SSL certificate on your server when trying to access the site over HTTPS.

### The Problem

This can occur when:

If you’re experiencing this issue, then it’s highly likely that you need to fix either the first or second error. 443 being closed would be a very apparent error that would likely manifest before hitting a 526.

### The Solution

Provision an SSL certificate.

### Method #1

If using our DNS API integration, you can follow this article:

Provisioning an SSL for a domain using DNS API Domain verification

### Method #2

If not, turn off the Cloudflare proxy and wait until your DNS records are pointing to your servers IP address worldwide – you can check this here:

https://dnschecker.org/#A

Then retry for another SSL.

### Method #3

If you need to provision an SSL before setting the Cloudflare API is not connected to your GridPane account (for example, it’s the client’s own Cloudflare account), you can use the DNS API Proxy Challenge method:

Provisioning an SSL for a domain using DNS API Domain verification by Proxy Challenge

NOTE: If you’re provisioning an SSL for a subdomain and using Cloudflare’s proxy, our system may have turned on the Forced SSL setting for this website within your Cloudflare account.

More info on troubleshooting 5XX errors can be found here on Cloudflare’s website:

Troubleshooting Cloudflare 5XX errors

 

## DNS API SSL Error: “Add txt record error”

This is typically a misconfiguration error when setting up your challenge records, but we’ve seen this error on regular DNS API SSL attempts as well.

If these records exist, then Let’s Encrypt will be unable to add this txt record again, and the SSL will fail.

For Proxy Challenge SSLs, you only need to add CNAME records at the unmanaged domain. Let’s Encrypt will add the verification records directly to the challenge domain you’ve set inside your DNS integration settings. It will then automatically remove them again afterward.

Full details can be found in this section of the proxy challenge article:Set DNS Challenge records at your site Domain DNS provider

In the logs, the error will appear like so:

```
-------------------------------------------------------------------Challenge Alias: yoursetchallengedomain.com-------------------------------------------------------------------_acme-challenge.example.com CNAME: _acme-challenge.yoursetchallengedomain.com.yoursetchallengedomain.com.199.199.199.19_acme-challenge.www.example.com CNAME: _acme-challenge.www.yoursetchallengedomain.com.www.yoursetchallengedomain.com.199.199.199.19-------------------------------------------------------------------Only _acme-challenge.example.com has CNAME _acme-challenge.yoursetchallengedomain.comproceeding to Dry Run for this domain only....(timeout after 300s max)[Sat Feb 26 19:44:39 GMT 2022] Using ACME_DIRECTORY: https://acme-staging-v02.api.letsencrypt.org/directory[Sat Feb 26 19:44:40 GMT 2022] Using CA: https://acme-staging-v02.api.letsencrypt.org/directory[Sat Feb 26 19:44:40 GMT 2022] Single domain='example.com'[Sat Feb 26 19:44:40 GMT 2022] Getting domain auth token for each domain[Sat Feb 26 19:44:41 GMT 2022] Getting webroot for domain='example.com'[Sat Feb 26 19:44:41 GMT 2022] Adding txt value: 8SRhUZ4vjMJHkf0w9etgH344mehMC5ig7ovRbDk for domain: _acme-challenge.yoursetchallengedomain.com[Sat Feb 26 19:44:42 GMT 2022] Adding record[Sat Feb 26 19:44:43 GMT 2022] Add txt record error.[Sat Feb 26 19:44:43 GMT 2022] Error add txt for domain:_acme-challenge.yoursetchallengedomain.com[Sat Feb 26 19:44:43 GMT 2022] Please check log file for more details: /root/gridenv/acme-wildcard-configs/staging/example.com/acme.sh.log--------------------------------------------------------------------Cert Provision Failed--------------------------------------------------------------------
```

If you’re seeing the same error in your log, please remove the _acme.challenge records from the domain and then try again.

 

## DNS Records Look Correct, but SSL Provisioning Still Fails (Check AAAA)

If your website’s A records are set correctly pointing to your server, AND they are live worldwide, then you may have conflicting AAAA records.

AAAA records are used for IPv6 addresses, and if these exist they may be pointing to an IP that is not used by your server.

### Diagnosis and Solution

Check your DNS settings for AAAA records for your URL and remove any not pointing towards your server. These are not necessary.

 

 

## SSL Support

SSL Certificates Failures
For assistance with SSL certificate related issues, please ensure you attach the info from your SSL provisioning logs when contacting support/posting in the community forum so that we can quickly assess what's going on and assist you as fast and efficiently as possible.
How to Create a Support Ticket
DNS Checks / Console Output / Screenshots
Please provide as much relevant information as possible - check if your DNS is live,  check console output on your site (right click > inspect element > console), and attach any relevant screenshots of errors.

Too Many Redirects Error
If you're using Cloudflare with GridPane, please ensure you have the correct SSL settings to prevent redirect errors:How to use Cloudflare SSL with GridPane
SSL Locks and Rate Limiting
If multiple SSL attempts fail, GridPane will place an SSL lock to prevent you from getting rate limited by Let's Encrypt. It's important to assess why your SSL's are failing and correct the issue. Learn more about rate-limiting and how to remove locks here:GridPane SSL Locks and Let’s Encrypt Rate Limiting
SSL Troubleshooting Guide
This article will help new users prevent common SSL issues, and learn how to diagnose the more complex ones.
Diagnosing and Fixing SSL Certificate Issues
SSL Renewal Failures
If you're receiving notifications that one of your SSL certificates has failed to renew, Let's Encrypt will return the exact reason for failure inside the Certbot or Acme monitoring logs.

Monit SSL Renewal Failure Notification in the Dashboard or Slack
Mixed Content / No Padlock
If you've provisioned an SSL but don't see a padlock, please check for images and/or other content being served over HTTP instead of HTTPS. It's likely you need to update your database to serve links over HTTPS:
Why Am I Not Seeing a Padlock on my Site?

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

