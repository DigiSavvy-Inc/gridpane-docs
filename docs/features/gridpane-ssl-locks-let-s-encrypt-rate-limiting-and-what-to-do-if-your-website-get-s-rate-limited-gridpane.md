# GridPane SSL Locks, Let’s Encrypt Rate Limiting, and What to Do if Your Website Get’s Rate Limited | GridPane

# GridPane SSL Locks, Let’s Encrypt Rate Limiting, and What to Do if Your Website Get’s Rate Limited

 

10 min read 

In order to prevent your websites from getting rate limited by Let’s Encrypt, GridPane has created a 3-attempt limit fail-safe that requires manual removal after 3 unsuccessful SSL attempts.

This article will explain why we’ve put this in place, the steps to remove it, and how to avoid it from happening altogether.

Also, you can only provision one SSL at a time on GridPane. We have a lock in place to enforce this to ensure that the process runs smoothly, and isn’t negatively affected by trying to provision multiple SSL certificates all at the same time.

### Table of Contents

 

## Part 1. An Introduction to SSL Rate Limiting

Let’s Encrypt provide an awesome free SSL, but like anything that’s free, they have (and absolutely need) systems in place to prevent abuse.

This comes in the form of rate-limiting. We don’t want that to happen, and as long as you are following our documentation, it should never happen to you, but as a precaution, we also have a locking mechanism in place to make sure you don’t accidentally hit a limit without realizing.

### Let’s Encrypt Rate Limiting Criteria

Too Many Failed Attempts for a URL: You get 5 attempts to provision an SSL for a website (whether subdomain or root domain), which should be plenty. If you fail 5 times in a row, you’ll be blocked from re-attempting for another SSL for your website for 7 days (see part 5 for your options if you do get rate limited).

Too many SSL attempts for an IP: There are also limits on the number of SSLs that you can provision for an IP address over a set time. Currently, it is a maximum of 10 SSL certificates per IP every 3 hours, but this is subject to change (see their documentation for more details). This may occur if you’re migrating a WaaS network into GridPane and you need to provision SSL certificates for lots of subsites.

Other limits also exist, but it is extremely rare that you would ever run into them. You can learn more about Let’s Encrypt rate limits here: https://letsencrypt.org/docs/rate-limits/

### GridPane’s SSL Locks

We’ve implemented a system that will lock and prevent SSL provisioning attempts from proceeding once you fail 3 times in a row.

Removing the lock is simple, but we put this in place to ensure our users can’t hit the Let’s Encrypt rate limit by continually re-attempting again and again until you hit their limit and lock you out.

 

## Part 2. Avoiding Locks/Rate Limiting

When an SSL attempt fails, you can easily find out the exact reason for the failure by checking your SSL log. In 95% of cases, this is related to your DNS records not pointing to your server’s IP address.

The SSL log will detail what went wrong and what you need to do in order for your SSL to provision correctly.

### Always check your logs

You should check your log immediately after the first failed attempt.

To locate and view your SSL log, head to your Sites page inside your GridPane account and click on your website’s domain name to open up the configuration modal.

Next, click through to the logs tab and click the button as outlined below to open up your SSL log:

This will open your log directly inside of GridPane, and you can view your latest SSL attempt by scrolling to the bottom. We’re looking for the reason for the failure, and that will look something like this, listed under “IMPORTANT NOTES”:

Here we can see that the reason for this particular failed attempt is as follows:

```
To fix these errors, please make sure that your domain name was
entered correctly and the DNS A/AAAA record(s) for that domain
contain(s) the right IP address.
```

The reason your SSL attempt failed may be different, however, this is by far the most common.

### If using a Proxy Service (e.g. Cloudflare) you may need to temporarily deactivate it

If you’re using a proxy service, for example, Cloudflare with orange clouds turned on, then Let’s Encrypt may not be able to verify that your domain name and server IP match up.

To check your DNS worldwide, you can use this website:

https://dnschecker.org/#A

When attempting to provision an SSL without either the DNS Made Easy or Cloudflare API, ensure that your A record and server IP address match before re-attempting.

### If using Cloudflare/DNS Made Easy API, check their status page

If you’re attempting to provision an SSL via Cloudflare API and it’s failing, then it’s highly likely that this is due to an outage or active maintenance at Cloudflare. You can check their status page here:

https://www.cloudflarestatus.com/

The same goes for DNS Made Easy. You can check their status here:

https://dnsstatus.com/

 

## Part 3. Removing GridPane’s SSL Lock

If you’ve experienced a lock, you’ll see a message that reads:

```
SSL Fail for: 
yourdomain.com
System detected too many failed attempts, provision is temporarily locked.
```

To remove this lock, you’ll need to SSH into your server and remove 3 files. Don’t worry, this is quick and easy and the following steps will walk you through it.

### Step 1. SSH into your server.

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Navigate to your websites log directory

Run the following command to navigate to your websites log directory, switching out “site.url” with your websites domain name:

```
cd /var/www/site.url/logs/
```

Example:

```
cd /var/www/gridpane.com/logs/
```

### Step 3. Remove 3 log files

To view the contents of this folder, run this command:

```
ls -l
```

Here, there will be three log files that look like this:

The names of course will be based on your domain name, but the key part is the “-ssl_fail-” as you can see highlighted in the image above.

To remove the lock, we need to remove these files. You can do so with the “rm” command, followed by the file name. Here’s what it looks like for the 3 files in the image above:

```
rm examplewebsite.com-ssl_fail-1.date
```

```
rm examplewebsite.com-ssl_fail-2.date
```

```
rm examplewebsite.com-ssl_fail-3.date
```

Alternatively, remove them all at the same time with this command:

```
rm examplewebsite.com-ssl_fail-*.date
```

We can make sure the files have been removed with the ls -l command again:

```
ls -l
```

As you can see below, I ran the rm command above, and on rechecking the contents the files are no longer there.

 

## Part 4. Checks: Set Things Up Correctly and Try Again

At this point, you can re-attempt to provision your SSL. Make sure that you have followed the instructions above and have confirmed and fixed the issue as outlined in your SSL log. We can’t help you if you’re rated limited by Let’s Encrypt.

More often than not it’s just a case of correcting your DNS settings. You can learn more about DNS here:

Setting DNS Records

If you’re simply not sure, you can shoot us a message on support.

If you have everything set up correctly, your SSL should be successful.

 

## Part 5. Workarounds: What to Do if You’ve Been Rate Limited by Let’s Encrypt

If you’ve been rate limited due to too many attempts on a server IP address, then you simply have to wait until the 3-hour limit has passed before you continue and try again.

If you’ve been rate limited by Let’s Encrypt due to too many failed attempts there is nothing that our team can do to resolve this for you. You won’t be able to run another attempt for an SSL for 7 days until the limit has been lifted.

However, as all SSL attempts apply to very specific criteria, there may be avenues available to you to get an SSL certificate.

### Option 1. Provision a Wildcard SSL Certificate

This is the best available option.

If you attempted a regular SSL certificate on your website and got rate limited you can use our DNS API integration to provision a Wildcard SSL instead. If the website DNS isn’t managed in either your DNSME or Cloudflare account, you can still provision a Wildcard SSL using the proxy challenge method.

Why this works: The original SSL attempt will have been specifically for either the root and www, or just the root. This specific configuration constitutes an “exact set of domains”, and this set has been limited. However, the wildcard is a different configuration that also includes all subdomains and this doesn’t match the previous set of domains. Therefore, this new set of domains hasn’t yet been rate-limited and is still eligible for an SSL certificate.

Here’s an example rate limit notification that you would see in your SSL log to illustrate:

```
[Mon Jan 24 15:00:00 UTC 2022] Create new order error. Le_OrderFinalize not found. {"type": "urn:ietf:params:acme:error:rateLimited","detail": "Error creating new order :: too many certificates (5) already issued for this exact set of domains in the last 168 hours: website.com: see https://letsencrypt.org/docs/rate-limits/","status": 429}
```

### Option 2. Clone the Website to another server

This may only work if your website had no existing DNS records and failed due to this.

Cloning the website to another GridPane server means that the site will now have a new IP address, and you can attempt to provision another SSL.

### Option 3. Provision for the Root Only (or root and www if the previous attempt was only for root)

If your SSL attempts were for both root and www, you may still be able to try for a new SSL that covers root only. This is less than ideal but it’s better than waiting 7 days with no SSL, and it works as it is different from the original set of domains. You will need to remove your www record and attempt for an SSL using the webroot method.

If you’re lucky, the reverse may also be true if you originally only attempted for root, and not www. Here you would need to ensure both your root and www DNS records are resolving correctly or use the DNS API method.

 

 

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

