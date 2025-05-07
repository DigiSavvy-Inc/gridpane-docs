# The OWASP Top 10 and GridPane WordPress Security Options | GridPane

# The OWASP Top 10 and GridPane WordPress Security Options

 

10 min read 

 

### Written By Thomas Raef

This article was contributed by Thomas Raef, the founder of  WeWatchYourWebsite.com. Thomas runs a website protection, monitoring and malware removal service and is one of a very, very short list of people who we recommend for this service.

## Introduction

The OWASP Top 10 is a list of the 10 most common website/application vulnerabilities compiled by the Open Web Application Security Project (OWASP). It’s updated every 3-4 years and offers a great look into the type of vulnerabilites that your website may face, and how hackers/malicious bots etc may look to attack your websites/s.

Enter Thomas

 

## 1. Injection

The majority of defenses against injection attacks rests solely on the developers.

But, for many web applications (WordPress) injection attacks can be:

GridPane does a good job of blocking SQL injection by their 6G and 7G firewalls which blocks many strings used in SQL injection. The rest of the defense for SQLi is up to the developers of themes and plugins.

Some will not agree that XSS is an injection attack, however, it is injecting script into the code, so it is considered an injection attack.

The GridPane Nginx configuration includes these security headers:

These headers add a lot to the security of your website.

The first header will prevent MIME-sniffing a response different from the declared content-type. Sometimes hackers will attempt to override the declared Content-Type and process the data using an implicit content type. This is mostly for sites that allow user uploaded content. They can upload content that is thought to be safe, then override that declared content-type with their own content-type and viola! a hacked website.

There are many bounty hunters making large sums of money using this very technique.

The second one allows pages to be served in a frame of a page on the same site. If any external sites try to load the page in a frame, the request is denied.

The final header option prevents the browser from rendering a web page if a potential cross-site scripting reflection (non-persistent) attack is detected.

All of these headers in the GridPane Nginx configuration files are great and highly effective methods of making your sites more secure.

 

## 2. Broken Authentication

This can be in the form of:

Typically these areas are controlled by the CMS, but these areas also include your server authentication and GridPane account authentication.

GridPane provides easy installment of Fail2ban. A failed login is a good sign of an attack. Kick them to the curb fast.

Fail2ban parses your log files looking for indications of an attack on your authentication system. As an attack is recognized, Fail2ban will insert a new rule in IPTABLES which will block the IP address of the attack. The block can last a preset amount of time, or it can be permanent.

Fail2ban works to prevent credential stuffing and brute force attacks. GridPane provides detailed documentation on Fail2ban.

You can also implement 2 factor authentication, or captcha.

For weak passwords, GridPane suggests iThemes Security, which in my opinion is a solid solution. iThemes also allows you to set password expiration and a maximum password age.

 

## 3. Sensitive Data Exposure

As it relates to web applications, this could be as basic as allowing directory browsing, which is easily prevented in Nginx.

This also includes forcing all traffic to https instead of easily readable http.

By default, Nginx, which is what GridPane supports, automatically disables directory browsing. If there is a folder you create that you don’t want easily browsable, simply create an empty index.php file and place that in the directory. Done.

Delete all phpinfo files. If you don’t already know, this file is used to diagnose problems. The problem is, it provides information about your PHP configuration. While deleting this file is considered “security by obscurity”, it is an effective way to prevent providing too much information, or preventing sensitive data exposure.

GridPane, implements HTTP Strict Transport Security for you, which is key to preventing sensitive data exposure.

If you look at your headers, you’ll see:

Strict-Transport-Security: max-age=31536000

This is called, “HTTP Strict Transport Security” (HSTS). This setting helps protect websites from Man-In-The-Middle (MITM) attacks and cookie hijacking. It forces the use of HTTPS.

The long number at the end specifies the amount of time the browser will only access the server in a secured manner. It’s how many seconds are in a year. So, all future requests for the next year (non-leap year) will only use HTTPS.

Other bits of sensitive information that hackers sometimes look for are:

These are all 403’d nicely by GridPane.

 

## 4. Broken Access Control

This is limiting what can be accessed on your sites.

Hiding the login page to your WordPress site would be a good example. It’s considered security by obscurity, but the truth is, if the hackers can’t find it, they can’t abuse it.

Using two factor authentication is a great way to prevent Broken Access Control exploits. Use on everything, from account access to WordPress login.

GridPane provides an easy management system for handling SSH keys. Use it.

 

## 5. Security Misconfiguration

Some common areas are:

Quite often people may have a form on their site that is no longer used. They don’t remove it, and many times don’t update the form plugin, but there it sits – open to the public.

As it’s commonly said, just because you don’t need it, doesn’t mean the hackers won’t use it. Get rid of it. This one is on you.

Using default login credentials is still prevalent in today’s environment and it’s 2020! Usually it’s a dev site or staging site and people think hackers won’t look there. Log files show that hackers frequently scan URLs looking for: staging.domain.com, dev.domain.com and many other variations. Security should be applied to ALL sites. ALL.

Server patches are typically handled by GridPane. Ubuntu and Nginx updates are handled by them on a frequent basis.

Files should have 444 or 644 permissions and all folders should have 755. End of story. 444 is fine for some files, but typically we set all files to 644.

 

## 6. Cross-site Scripting (XSS)

This can be handled easily with Content Security Policy. That’s what CSP excels at. However, setting up and monitoring a well-designed CSP is not easy. GridPane has the basic CSP in the Nginx config file, but it needs to be custom designed for each site depending on what theme is used, what plugins are used, etc. WeWatchYourWebsite has created and tested a CSP creation tool that also includes monitoring for any violations.

With CSP, you whitelist all CSS, javascript and other functions. A hash of each one is created. This hash is checked as a visitor comes to your site. Actually their browser checks the hash, so this layer of security does not consume any resources on your website.

Many of you have heard of the MageCart attacks where the hackers inject code into a 3rd party application that processes credit card transactions. If not, and you are responsible for an e-commerce site, you best search for MageCart attacks.

These could have all been prevented with a “properly” designed CSP.

A properly designed CSP would have had hashes for each javascript file, whether hosted on your site or somewhere else (think Google Analytics javascript). The problem with many of the CSP’s is that they whitelisted the Google Analytics domain. They should have had a hash created for the Google Analytics javascript.

That way, the first person, after the credit card skimming code was added and to browse a website with CSP wouldn’t have been able to check out as the hash would have been different from what the CSP whitelisted AND with reporting setup, it would have notified someone that the javascript was changed.

End.Of.Story.

CSP is not just designed for e-commerce sites. Look at the source of your website after it’s been rendered in your browser. Look how many external references there are to javascript and sometimes CSS files. Everyone of those should have a hash created. That way, if a hacker were to inject code into any one of those files, it would be blocked and a notification would be sent to alert you that a file has changed.

 

## 7. Using Components With Known Vulnerabilities

This would be like when many sites were infected due to timthumb.php, or sites were infected due to fckeditor. Those are components.

Some may put plugins in this category as well, but I don’t believe that was the intentional purpose of this category. But for this document, we’ll include plugins.

The world of components moves so fast. What was safe yesterday, is being exploited by the thousands today. It seems like patching is a way of life.

The question becomes, “How can I be certain all my plugins are updated?”

One of the easiest ways is to add some code into a mu-plugin (Must-Use).

If you look in wp-content you’ll see a folder named “mu-plugins”, if not, create it.

Mu-plugins was originally created when multi-site was first created. It allowed admins to specify certain plugins that all sites in the farm would use. Now, it refers to “Must Use”.

Must-use plugins do not show in the list of plugins in wp-admin. They cannot be deactivated other than by deleting the file in the mu-plugins directory. Must-use plugins are always on and cannot be “accidentally” deactivated. They are loaded before normal plugins and are activated in alphabetical order.

Only files directly in the mu-plugins folder will be run. No sub-folders allowed, unless they’re specifically called from a function in the main file.

So, what do we put in there?

I create a file called auto-updates.php. Inside there, add this code:

```
<?php
```

```
add_filter( 'auto_update_plugin', '__return_true' )
```

That’s it!

Now, your plugins will always be updated.

I know, I hear it already. “But what if a plugin update breaks the site?”

You have two options, you can take that risk, or take the risk of having your site hacked because you didn’t want to trust the plugin developer to write compatible code.

The choice is yours.

 

## 8. Insufficient Logging and Monitoring

Assume compromise.

OWASP recommends logging “auditable” events such as: logins, failed logins and high-value transactions. They also recommend logging warnings and errors.

Hackers will typically “recon” a website. This means they’re looking for ways to exploit a vulnerability and gain information or access.

As they “hit” your website, rarely is it successful on the first try. When it fails, it might leave error messages in your error_logs. These must be monitored. The same is true with login and failed logins. Rarely is the first one successful. If it is successful, then you have to look at how they obtained the correct username and password.

Fail2ban is great at blocking repeated attempts. It reads your log files and will add IP addresses to a block list. This isn’t foolproof though. Hackers know all about Fail2ban and they will purposely use as many as 50 – 100 different IP addresses. They’ll even spread them out over extended periods of time to evade blocking.

More can be done here.

OWASP also recommends not storing the logs only locally. They should be streamed off-site. This way, if your server should self-destruct, you have copies elsewhere for root cause analysis, etc.

GridPane does setup logging, however it is up to you to gather them, store them off-site and read and analyze them.

 

 

### If you enjoyed this article...

Thomas has contributed multiple articles to the GridPane knowledge base, all of which are listed below:

The OWASP Top 10 and GridPane WordPress Security Options
Server Provider Attack Warnings: How to Find Brute Force Malware
Updating Cloudflare Real IPs

## OWASP 9 and 10

2 Items were left off the list: XML External Entities and Insecure Deserialization. They were intentionally left off because this report is about how GridPane addresses the OWASP Top 10. These two areas are strictly programming concerns.

That’s a wrap!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

