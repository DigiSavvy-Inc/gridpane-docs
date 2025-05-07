# Sites are Down! Part 1: Here’s What Everyone Needs to Know | GridPane

# Sites are Down! Part 1: Here’s What Everyone Needs to Know

 

10 min read 

## Introduction

If your websites have been running smoothly for more than a few days, the chances of them running into a serious issue or “going down” is incredibly rare. However, a few key pieces of information can be incredibly empowering for if things do ever go wrong

If you’re using best practices and you use your staging to do your dev work and test updates, and you have backups running both locally and remotely, and you don’t ignore your notifications in your GridPane account, you’ll rarely ever see any kind of issues.

### The Goal of this Article

This article will go cover the fundamentals of what everyone running self-managed hosting should know about troubleshooting “site down” and “server down” issues.

This article is NOT about issues that could potentially occur after a migration. We have a separate troubleshooting doc (Diagnosing Migration Issues) that covers every known issue.

This is for sites that were working fine, and now suddenly are down. These are going to be one of the following: –

We’ll cover the basics of why these things happen here in Part 1. In Part 2 we cover the practical troubleshooting side of things.Sites are Down! Part 2: Practical Troubleshooting

 

### Table of Contents

 

## 1. Your DNS is incorrect

A good portion of the issues that we see on support are due to the DNS records not pointing to the GridPane server. Everyone should bookmark the following link – it’s incredibly useful whenever you make a DNS change:https://dnschecker.org/#A

All of our team use this website at least several times per day.

 

## 2. Your server provider / DNS provider is down

Next in your hosting bookmarks should be all of your provider status pages – DNS, Servers, SMTP, Let’s Encrypt, and anything else that you rely on. True server down issues are usually maintenance windows. Here are some of the common ones:

Let’s Encrypt / Cloudflare / DNSME / DigitalOcean / Vultr / Linode / UpCloud / AWS / Hetzner / OVH / SendGrid / Postmark

If a server is down, our application won’t be able to connect to it. You can verify this by clicking the refresh icon next to your server in your account – it will give a “disconnected” status we can’t access it.

 

## 3. Your cache needs clearing

If your website appears to be broken, you can always quickly check whether the issue you’re seeing is related to the cache by adding a query string to the URI. For example: website.com?123 is what I usually go for. If the website is all good, you can clear the cache.

 

## 4. Your file permissions are incorrect

If you’ve edited or uploaded files as the root user, the permissions for those files will be set to the root user. This will make them inaccessible to your website. Run a permissions fix over on the Tools page in your account – it will take care of this for you and ensure that all of your website files have the correct permissions in a matter of seconds.

 

## 5. The disk space on the server is full

Letting your disk space fill up can have serious consequences. At best, MySQL will go down, and all your sites will go down with it. At worst, you’ll suffer irreversible MySQL damage. In the latter scenario, you’ll need to fall back to your server provider snapshot.

This is why Monit sends notifications every 2 minutes once the disk space on a server gets close to 100%. If you’re using 70-80% disk space usage on a server it’s probably time to either do some spring cleaning (database cleanups, remove unnecessary backups etc), or scale up the server (or increase only disk space if the provider allows for that).

Usually, when we see this it’s a result of completely ignoring all notifications for extended periods of time and could have been entirely prevented. On a couple of extremely rare occasions, a backup plugin has gone crazy, and run over and over filling up disk space.

 

## 6. Codebase Issues

Codebase issues can break parts or all of your site. Fatal PHP errors due to not having enough memory, code errors, corrupt or missing core files, or core files in the wrong place (e.g. wp-config.php inside /htdocs) can all take a site down.

Some plugins may “go rogue” and cause issues as well.

While 502 and 504 errors can certainly be caused by high load, the vast majority that our team have seen over the years are codebase specific.

Common issues include database table locking, unusually high CPU consumption due to a plugin repeatedly trying to execute a task, or long-running requests causing a build-up that hogs the CPU, and causes a backlog of requests the server can’t keep up with. For example, in the four years I’ve been managing my own servers, I’ve had Wordfence go crazy 3 times, running the CPU through the roof back way back in 2018 one time, and locking up a database on two other occasions (these are actually the only issues I’ve experienced).

Restarting PHP and MySQL (in the case of extreme table locking/sleeping tables) often immediately fixes these issues, but they don’t address the root cause.

 

## 7. .htaccess misconfigured (OLS only)

A misconfigured .htaccess is a quick way to take your site down, resulting in anything from 500 errors, missing internal pages, and potentially many other undesirable issues.

A backup of your .htaccess is stored in your websites /htdocs directory. You can use that backup to quickly bring your site back online.

 

## 8. Locked Database Tables and/or Sleeping Queries

Database table locking is a common cause behind many 502 and 504 errors. Sleeping queries less so in our experience, but they can have the same effect – the site times out while trying to read from the database.

Database tables locked due to a plugin (all sites affected – restart MySQL).

Sleeping queries in the database due to a plugin (site specific – restart MySQL).

 

## 9. Database corruption

Database corruption usually occurs when core/theme/plugin files have become corrupt, or if something went terribly wrong installing a new theme or plugin or uninstalling them. Disk space filling up and/or an operation being interrupted are other potential causes. Usually this is a quick and simple fix. For the one in a thousand where this doesn’t work, a backup restore would be the way to go.

 

## 10. Site is “Insecure”

SSL related issues – expired, www missing, forcing HTTPS from inside WP with no SSL. These can be easily solved by ensuring that your DNS is correct or that your API key is still correct, and either renewing the expired SSL, or provisioning a new one.

If the “www” is missing, you will need to provision a brand new one – renewing won’t add www to a certificate if it doesn’t already exist.

 

## 11. Server is Overloaded

If the server isn’t big enough to handle the current load you’ll experience 502 and/or 504 errors. In extreme cases you may even see the Redis service go down.

Make sure server page caching and object caching are on, and turn on Fail2Ban integration to ensure bots aren’t consuming resources that could otherwise be used by your website/s.

Depending on the size of the server, the amount of traffic you’re dealing with, how much traffic is bypassing the cache, your code base, how capable your CPU is, you may need to optimize your PHP and MySQL configurations to get better performance. Our stack will work incredibly well for 90% of all sites out of the box, but high traffic can uncover potential bottlenecks.

Making a few tweaks to optimize your database and PHP worker settings can sometimes prevent 502/504 errors without needing to increase the size of your server.

 

## 12. Nginx/OLS Misconfiguration

Syntax errors happen for one of two reasons – there’s a file that Nginx/OLS is trying to load, and it’s no longer there, or there’s an actual error in the code.

Checking the syntax before reloading Nginx will let you know if there are any issues immediately. On OLS, that’s not the case, and you can only find out if a syntax error after the fact. Fortunately, undoing what you may have just done is simple.

.htaccess misconfiguration can also cause syntax errors as well.

 

## 13. Services are down (MySQL, PHP, Nginx, OLS)

If for some reason a service is down, Monit will automatically attempt to restart it. If for some reason that fails, you can also try to restart inside of Monit by clicking on the name of the service, or running a quick command on the command line.

If it’s down due to a syntax issue, this will need to be corrected before attempting a restart.

 

## 14. PHP worker misconfiguration

PHP worker misconfiguration can cause or amplify a few different issue. The one issue it can directly cause is consuming a huge amount of RAM. This can lead to poor performance as your other services may not have enough memory to run efficiently, and instead run on disk which can lead to I/O wait issues.

Usually it amplifies codebase or MySQL related issues. For example, if you had 100 workers for a site, and you had a build up of 100 long running requests, this will completely consume your CPU and cause 502/504 errors for an extended period of time, or indefinitely until restarted as the backed up queue can never be worked through.

On Nginx you should have between 2-5 PHP workers per CPU core. If you have a super fast CPU and lean code base, you may be able to set 5. If you have a super heavy codebase and average CPU you may need to go as low as 2.

First restart PHP to clear out the queue. Then fix your worker configuration. Generally, this will only be an issue on Nginx, as the OLS defaults aren’t something you’ll likely ever change.

 

## 15. Severe CPU Steal

If you’re experiencing high CPU, regardless of whether you expected it or not, one the things to always check for is CPU steal by running top on your server.

This is where another VPS on your server is using more than it’s fair share of available CPU, infringing on your own resources. Here all you can do is reach out to your provider and let them know what’s going on. They are usually quick to resolve such issues.

 

## 16. You’ve been hacked

Hacks are rare on GridPane, and if you’re using our Fail2Ban integration and block wp-content php security measure, the chances of being hacked or suffering serious damage due to a hack are incredibly slim.

That said, live vulnerabilities in core/theme/plugins can lead to a compromised site and have disastrous effects, resulting in anything from severe database issues, to files going missing, or malicious code being injected throughout your site. Your site may even be used as a part of a botnet to attack other sites and servers.

 

## Next up! Part 2: Practical Troubleshooting

In part 2 we’ll cover the practical side of things like checking your database for table locks, checking for CPU steal, database corruption, etc.

All of this information already exists inside of the 500, 502, 504 documentation, and the docs that you can find here:Diagnose and Fix Common Issues

To continue to Part 2, click here:Sites are Down! Part 2: Practical Troubleshooting

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

