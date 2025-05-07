# WordPress Security 2023: Securing Multiple Banking Websites | GridPane

# WP Security 2024: Securing Multiple Banking Websites Built on WordPress

 

39 min read 

 

### 2024 Notice

Since publishing, there were a few things that I would now do differently. This article has now been updated to include these changes.

A case study on how I secured two WordPress websites for a multinational bank, from start to finish.

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='597'%20viewBox='0%200%201024%20597'%3E%3C/svg%3E)

### Table of Contents

 

## Introduction

We often get asked about WordPress security. What steps should I take to secure my website? Should I use a security plugin? Which security plugin? Should I use Cloudflare?

All good questions, but as WordPress websites and hosting environments can vary wildly, there’s no answer that will apply to all situations (and there’s also more than one way to get the job done).

In this post/article/guide, we’re going to look at one of my own previous projects – a series of landing pages for a multinational bank. We figured this would make for a pretty interesting case study on how to lock down and secure a WordPress site from start to finish. As you can imagine, security was incredibly important for this project, and in this article we’ll look at the different security concerns I prepared for, and how I put all of it into practice.

Below covers the key considerations that you can use to implement your own security plan for all of your own projects.

If you’re looking to delve deeper into the threats lurking beyond your website’s borders, this article will serve as a good starting point.

### The Project

The Website: Develop a set of 4 landing pages across two WordPress installations to promote personal and business-related banking assistance/services during the coronavirus crisis.

Hosting: This was later added to the scope when their IT team came back and told us they needed 3 months to prepare. That was ridiculous, and we didn’t expect the campaign to last longer than 2 months at the time, so after some discussion, I took on hosting the websites as well (including ongoing maintenance and DNS management).

With the exception of the Content Security Policy (more in part 7), provisioning a brand new server, importing the two websites, and implementing the security setup outlined below took a grand total of approximately 35 minutes.

### Security Strategy: Prevention and Detection/Recovery

When planning your security strategy, you may find it useful to split your plan into two parts. The first part is Prevention, and the second is Detection/Recovery.

Prevention is everything you implement to keep your websites secure in the first place. The bulk of this article is about prevention and includes practices such as implementing a web application firewall (WAFs), server and application hardening, and security hygiene.

Detection/Recovery is emergency planning for the worst-case scenario. If, despite all your efforts, your site still gets hacked, how will you detect it? And how will you minimize the risks of reputation damage and more, and get the site cleaned up and back in business as quickly as possible?

 

 

### What is a Web Application Firewall (WAF)?

In a nutshell, a WAF acts like a security guard in front of your website, but instead of an allowed-guests list, they have a do-not-allow list. This do-not-allow list is a set of rules designed to filter out bad requests and malicious traffic and then block this malicious traffic before it can reach your website. A WAF should be a key component of your security strategy.

### DNS, Server, and Application Level Security

When approaching WordPress security, the earlier in the DNS > Server > Application chain you can implement security, the better.

If I can block attacks at the DNS level, then they never even reach my server. If I can block attacks at the server level, then they’re immediately dropped and never reach my applications (applications = WordPress websites in our case). By approaching your security this way, you can prevent many different types of attacks before they even get the chance to compromise your site (as they won’t be able to get to it in the first place).

 

## A 2024 Guide to WordPress Security from Start to Finish

 

## Part 1. Organizational Level Security Policies & Cyber Hygiene

Good security starts with simple, basic security policies at the business/organizational level. This extends beyond just website security and is important for all aspects of business.

Exploiting website-level vulnerabilities or “Mr. Robot’ing” into a server aren’t the only ways to gain access to a website. Malware on a company computer could theoretically scrape usernames and passwords, steal authentication cookies (a huge but lesser-known problem) or grant backdoor access to a hacker who could steal all kinds of information. Banks, not surprisingly, have this down pretty well, but most businesses do not.

### Cyber Hygiene

The idea behind the phrase “Cyber Hygiene” is that just like you maintain good general hygiene habits day-in-day-out (taking a shower, brushing your teeth, etc), you should take the same approach to your IT and online systems “health”.

This includes ALL security as a whole.

I can enforce a strong password, but that’s not going to help if my client stores it in a text file on their desktop and someone steals their computer. Or even worse, sticks a post-it note with their username and password on their workstation monitor.

A little cyber hygiene goes a long way. In fact, research conducted by the University of Portsmouth for the UK government suggested that 80% of the cyber-attacks affecting businesses in the UK could have been prevented by the implementation of some basic security controls. It would be surprising if the same weren’t also true for most other countries throughout the world.

This is a conversation that I believe needs to be had with every client. Helping clients with their security will help you avoid potential future hassle, and it’s a good trust builder when you take on new projects.

### Avoid Public WiFi Networks

Your local coffee shop WiFi network is not secure, and neither is any personal data such as passwords, credit card numbers, client communications, etc. If using a public WiFi network to access your websites (or do anything of consequence), purchase and use a VPN to encrypt your information and keep yourself and your clients safe. Digg.com always has deals for super cheap.

 

## Part 2. Fundamental Website Security

There are a few fundamentals that every website should follow. Let’s take a look at these first.

### 1. Use a Quality Theme and Well Supported Plugins

I’ve always tried to be cautious of the way I build websites from both a security and longevity perspective. Good security starts from the ground up, and I built these websites using well-supported plugins and a well-supported theme.

Here I used the Genesis Framework with a custom child theme. It’s fast, very secure, and at the time, it was regularly updated. It was a solid choice for any WordPress website for well over a decade (and is still great).

Side note: There are many really great free themes, but there’s also no incentive for the developers of many of these themes to continue supporting them, which rules them out for me when thinking about a project’s longevity.

I also used a total of 9 plugins:

Two backup plugins, two design plugins, two caching plugins, and three security plugins. Crossed out are the plugins I would replace.

##### 2023/2024 Update

Today, I would replace or omit most of this.

I would not use Sucuri and would definitely not use WP 2FA like I originally did. I would, however, install these two security plugins:

Using three security plugins probably sounds overkill, but each serves different functions.

I also wouldn’t use any backup plugins. I’d stick with GridPane’s local and remote backups, and I’d download a backup of the site after launch and follow our own backup advice.

And yep, I used Elementor back then. If was I building these projects today, I would replace Elementor and the Genesis theme with Breakdance.

For SMTP, I used the GridPane SendGrid integration. This is a super simple, must-use plugin that tells WordPress to send transactional emails via my SendGrid account.

 

 

### Why no WordPress malware scanner plugin?

The conventional method of plugin-based malware scanning in WordPress is deeply flawed and I also just don't trust most of the security "suite" plugins out there. If you're interested in learning more about this topic, check out this research to see why everything you know about WordPress malware scanning is WRONG.

##### Additional Notes

 

### 2. Limited Administrator Access

There’s no upside to handing out admin access to people who simply don’t need it. The average person isn’t particularly security conscious, and the more you hand out access, the more insecure your websites become as a consequence. It also increases the chances of someone breaking something and no developer needs that kind of hassle.

The actual security term for this is “The Principle of Least Privilege“.

WordPress comes with multiple different levels of access that can help you give people the access they need to do their work, and at the same time limit their ability to do damage.

### 3. Enforce Strong Passwords and Appropriate Usernames

This applies everywhere, not just on your WordPress website. If you have weak security on your computer or computer systems as a whole, this opens up security vulnerabilities that could compromise your business (and WordPress site).

Usernames such as “admin” or “administrator” are asking for trouble. These are common targets and are not appropriate for production-ready websites in 2022.

Usually, I try to help other clients implement a strong password policy in their business. As I mentioned earlier, this is a great trust-building exercise, and it legitimately helps keep them safe over the long term.

Also, if a client ever does get hacked and you haven’t had a proper conversation about security, even if it was entirely their fault, they’re unlikely to see it that way. That’s a difficult thing for a relationship to recover from.

Here are the top 10 most used passwords according to: https://www.ncsc.gov.uk/news/most-hacked-passwords-revealed-as-uk-cyber-survey-exposes-gaps-in-online-security

##### So what is a strong password?

Guidance on this varies, but generally, the length of the password is the most important thing. The longer, the better. The character set is also a factor. The use of special characters is a lesser factor, but also still a good idea – at least according to the sources I’ve read, but I’d definitely encourage you to research further.

“Qwerty123456” is a terrible password.

“IloveridngthroughtheforestonaMOOse3timesaday?!?!floopAdoop” is a very strong password.

As is: “5J+UDLnWd%N?_dxxCZ2W4JrYGnJ9TqmPBg5AbQN?”.

There are multiple strong password generators online that you can use as the starting point for your passwords.

###### 2023/2024 Update

The Fortress plugin enforces strong passwords by default, as well as massively upgrading the out-of-date cryptography used by default in WordPress.

### 4. Don’t reuse passwords on multiple sites

Security breaches, unfortunately, are not uncommon – some huge companies over the past few years have gotten in trouble for data breaches. These include companies like Adobe, LinkedIn, eBay, Yahoo, and many more.

Also, unfortunately, using the same password for every website is absolutely common and seems to be becoming more of a problem day by day. If you or your clients are using the same password for your/their WordPress website, and another company experiences a breach, this now becomes a security vulnerability that could easily have been prevented. What’s worse is you may never see this one coming or figure out how it happened after the fact.

It’s also entirely possible that it’s already happened, and you don’t know about it. If you’ve never run a password check before, you should head over to haveibeenpwned.com to see if any of your accounts have been reported in a data breach (or several).

### 5. Two Factor Authentication (2FA)

2FA is an easy, effective way to lock down a site. No matter how secure a password is, there’s always a chance that it may be discovered. 2FA ensures that it’s impossible for an attacker to brute force their way into a website without both the password and your authentication method.

This is good practice, and we highly recommend that everyone use it.

###### 2023/2024 Update

Originally, I used the “WP 2FA – Two-factor Authentication for the WordPress” plugin. However, in light of Calvin Alkan of Snicco’s security research, I would never trust this plugin with any website’s security. Now, my 2FA is all handled by Snicco’s Fortress plugin, which is integrated at the server level with GridPane.

Fortress also allows you to enforce 2FA on different user roles, including administrator and editor roles, by default. When this is activated, administrator and editor accounts can’t be logged into without going through 2FA. If 2FA isn’t already set up for an account, it will provide an error notice stating that this should not happen.

This all means that if there’s a vulnerability in your codebase that allows attackers to create administrator roles for themselves on your website, they still wouldn’t be able to log in and exploit your site.

### 6. A+ Grade SSL certificates

Provisioning FREE A+ grade SSL certificates is a one-click task on GridPane, and both sites are, of course, using SSL certificates. Most quality web hosts will enable you to do this easily as well.

Site note: Cloudflare is my go-to DNS provider. I’ve used them for many years, and I’m a big fan of their service. GridPane has a Cloudflare integration built right into the dashboard, and using this, I was able to quickly and easily provision SSL certificates before setting the websites live.

 

## Part 3.1 Server Hardening and WordPress Hardening

GridPane takes care of a lot of security out of the box. You can learn more about the specifics in this knowledge base article: Default GridPane Security and Additional Options

I’ll be covering all of this below to share with you exactly what I’ve done to ensure these websites are as secure as possible.

### Server Hardening

All GridPane servers are hardened during the provisioning process. Ports are locked down, and Fail2Ban and the Linux UFW (uncomplicated firewall) are preconfigured. Access is SSH Key restricted and server security updates are automatically taken care of. We take security very seriously here at GridPane, and servers are secured immediately upon creation.

### SFTP and SSH access only

Secure server connections only. No FTP. No exceptions.

Some hosts still allow regular, insecure FTP connections, but in these cases, there’s usually little you can do about it. If this applies to you, you may want to contact your provider to see what kind of security measures they have in place to keep you safe. FTP compromises are rare, but there’s really no place for it on the modern web. SFTP does exactly the same thing, but it does it securely.

### Website Isolation

GridPane isolates websites by assigning them different system users on their creation. This is extremely important, as without this if one website were to get hacked/infected with malware, it could infect all other websites on that same system user – it’s one of the [many] major drawbacks of many, many shared hosting providers (and also multisites).

These are known as cross-site contamination attacks and cause a world of hurt on servers with many websites all on the same system user, compromising all of them in short order.

Keeping each site separated keeps them safe from each other. In my case, this server itself is also only used for the bank, and no other sites are hosted on it.

### Secure file and directory permissions by default

GridPane automatically sets files and folders with secure READ, WRITE and EXECUTE permissions. These permissions determine who is allowed to do what, and loose permissions leave your websites and servers open to attack.

GridPane automatically sets file and directory permissions correctly and provides a self-help tool that will help you reset any of your website’s permissions to ensure that any website you move to GridPane it’s all set correctly.

Learn more here: https://wordpress.org/support/article/changing-file-permissions/

### Secure PHP

GridPane defaults always set new websites to be created using an up-to-date version of PHP. At the time, this was PHP 7.4, but this has since reached its end-of-life, and the sites would have been updated accordingly.

This is an important one. PHP is fundamental to WordPress, and if the version you’re using is out-of-date, it means it’s no longer actively supported, and there are no more security patches coming.

Up-to-date PHP versions also offer significant performance improvements as well. You should always be using a supported version.

### HTTP Strict Transport Security

This needs to be implemented in combination with an SSL certificate.

GridPane, implements HTTP Strict Transport Security (once an SSL certificate is provisioned) by automatically adding this header to all websites:

Strict-Transport-Security: max-age=31536000

This protects against Man-In-The-Middle (MITM) attacks and cookie hijacking by forcing the use of HTTPS and preventing sensitive data exposure.

The “31536000” at the end is the number of seconds in a year. This instructs browsers to only access the server over HTTPS for the next year.

### Secure usernames and passwords by default

The websites both had secure login credentials from the moment they were created. One other user has editor access so that she can make tweaks without needing me – strong username and password of course.

### Disable directory browsing / System file protection

GridPane automatically prevents anyone from seeing any of the WordPress installation files (including all PHP files and dotfiles like .user.ini) and disallows access to readme.html, readme.txt, install.php, and wp-includes.

The reason this is important is that it prevents sensitive data exposure, which can be used in an attack against your website. The less information a hacker has to work with, the harder it will be to attack your site. For example, hiding your WordPress version ensures that you can’t be targeted specifically for the version of WordPress you’re using.

This technically falls under security by obscurity, which I regularly see people argue that this isn’t really security. However, attackers can and will target WordPress versions based on their known vulnerabilities, and hiding your WordPress version not only makes this more difficult but it also gives tools like Fail2Ban the opportunity to evaluate this behavior and ban accordingly (more on Fail2Ban in part 4).

### Secure wp-config.php

GridPane stores the wp-config.php file one level up from the htdocs directory. The wp-config.php file contains database usernames and passwords along with other sensitive information. By default, it’s kept hidden and protected.

### Block install.php

This WordPress core file is used to install WordPress, but WordPress is already installed, so it’s redundant. It’s also used by bots to identify a site as WordPress, so I’ve blocked it.

### Block WordPress OPML Links Functionality

WordPress allows links to be imported or exported using the OPML format via the wp-links-opml.php file. Hitting this page presents an XML output and details of a WordPress installation. Some bad bots will try this page when exploring your site for information.

Neither website is using it, so I’ve blocked this function at the server level.

 

## Part 3.2 WordPress Hardening 2023/2024 Update

In addition to all of the above, two more areas within WordPress can, and should, be much more secure. These are password cryptography and session management.

Forced routing is also a lesser-known and definitely underrated security enhancement.

And finally, our Git integration can be used to make the entire codebase immutable. This makes your WordPress codebase orders of magnitude more secure.

### Password Cryptography

By default, WordPress passwords are still hashed using md5. MD5 hashes are no longer considered secure. WordPress should have replaced this a long time ago.

Fortress, the security plugin, replaces this with its own implementation based on the libsodium core PHP extension. This is the most secure cryptography implementation in PHP.

### Secure Session Management

To provide some context on what sessions are actually are, here’s the breakdown from our Fortress documentation:

A major security issue is that an attacker can steal already valid cookies either via network communication or via malware on a user’s infected computer, and stolen cookies are sold to hackers in huge batches on the dark web. WordPress sites are wide open to these attacks, and neither Core or any other third-party security plugins have a solution.

At the time of writing, the Linus Tech Tips YouTube channel have just suffered a similar attack – detailed video here.

To wrap this up, Fortress dramatically improves session management across four dimensions (timeouts) to harden WordPress session security and make this kind of attack almost impossible. Further info can be found via the knowledge base article linked above.

### Forced Routing

GridPane makes it easy to force either root (https://) or www  (https://www) routing. At first glance, it may not be obvious how this could provide additional security, but forcing routing can prevent a pretty common attack.

As an example, Elementor had a serious vulnerability that allowed an attacker to turn on the user registration page (if disabled), set the default user role to administrator, and create an account for themselves that instantly has administrator privileges. From there they have full control of your site.

This was actively exploited, and one way it was exploited was to change the WordPress and site address URLs and redirect the hacked site to another website.

With forced routing, this would not have been possible.

### Immutable Codebase

By running an immutable codebase, you prevent any potential attackers (or even website owners) from being able to edit any WordPress files, including themes and plugins. Combining this with disabling PHP execution (more in part 6 below), means that an attacker can’t make malicious edits to run within WordPress or upload malicious files and execute them remotely.

In a nutshell, this locks down the entire WordPress codebase and keeps it secure.

 

## Part 4. Brute Force Protection

A brute force attack is an attempt to gain access to your website by systematically entering all possible passwords until the correct one is found and they’re able to login. It is literally sheer, relentless brute force hammering away at your login page. If left unchecked, this can put a tremendous strain on your server’s resources, similar to how a DoS attack works (more on this in part 5).

If you’re interested in digging into the topic, OWASP has a cool article that gives a few examples of different types of brute force attacks that you can check out here:https://owasp.org/www-community/attacks/Brute_force_attack

### Fail2Ban integration

Hurray for Fail2Ban! What a fantastic piece of software this is. If you’re looking to prevent brute force attacks, keep bad bots off your server, conserve server resources, and even block dirty dirty comment spam (mark a comment as spam, and Fail2Ban will ban that IP), Fail2Ban is fantastic.

We’re big fans of it here at GridPane, so much so that we have a direct integration with the excellent WP Fail2Ban plugin, which can now be activated with one click of a toggle. Additionally, we also have our own custom CLI for protecting wp-login.php and xmlrpc.php.

Learn more here: Configuring Fail2Ban to Prevent Brute Force Attacks

Fail2Ban looks for patterns of bad behavior, including things like failed login attempts, user enumeration (where a bot probes your site for information such as usernames – brute force attacks are essentially impossible without knowing a valid username or email address), and then bans the offending IP addresses. It does this exceptionally well.

I’ve also used GridPane’s GP-CLI to set up a strict 1 failed login only rule, which means that 2 failed login attempts = banned for 24 hours. Harsh but effective.

### Nginx Rate Limiting

Out of the box, GridPane places a limit on the number of requests that can hit wp-login.php at the same time. This can be changed, but the default limit of 1 hit per second to protect against brute force attacks offers decent basic protection. This means the page can only be accessed 60 times per minute per IP address (and not, for example, 1000 times per minute by the same IP).

The Nginx rate limiting will simply drop the request with a 503 error code. 1 hit per second is fine for my purposes.

### Summary: Brute Forcing These 2 Websites is Impossible

With the security setup that I’ve employed above, not to mention 2FA, a brute force attack on these websites would be a fruitless waste of time for any would-be attacker.

 

## Part 5. DoS / DDoS Protection

DoS stands for “denial of service.” This is where an attacker uses a single internet connection to flood a server with TCP and UDP packets. These packets overwhelm the server’s resources, rendering it unable to serve your website’s visitors, possibly causing it to shut down entirely. The goal is to take you offline, denying access to your website or network.

A DDoS attack is one of the most common types of DoS attacks. A DDoS attack uses multiple internet connections to target a single system, making it easier to overwhelm and take a system offline, as well as making the attack itself more difficult to mitigate. Larger-scale DDoS attacks can use thousands of connections to attack a server, and these often come from other compromised devices, also known as a botnet.

They can range anywhere from being a major pain in the ass to an absolute disaster, depending on the business being targeted. For example, a serious DDoS attack against a giant e-commerce store could result in tens of thousands of dollars in lost sales.

### Fail2Ban (Again)

Fail2Ban isn’t a cure by itself, but it can help to mitigate DoS and DDoS attacks by identifying bad behavior and then blocking the IP addresses that are hammering the server. It’s a good first line of defense, but hackers/attackers are well aware of Fail2Ban, and it’s unlikely that it will be able to provide enough protection against a massive attack.

### Disable XML RPC

XML RPC is an old, outdated, and insecure method of remotely posting to a WordPress website. These websites don’t use it, so I’ve disabled it completely at the server level.

There are many plugins that can do this at the WordPress level. However, this doesn’t prevent hits from reaching the server, and so it’s still possible to overwhelm a website by hammering xmlrpc.php if it’s not immediately dropped at the DNS or server level.

### Disable Concatenating Load Scripts

WordPress has a feature that concatenates WP-Admin JS and CSS. While this may seem innocuous, there are circumstances where this could be used to DoS a server, and in the age of HTTP/2 multiplexing, concatenating load scripts isn’t really necessary.

### GeoIP Restriction

GeoIP restriction is where you block traffic from specific countries so that traffic from those countries can’t access your website. It’s something I’ve considered implementing on these sites since the beginning, but with the bank being multinational and various people in different countries needing to review the site, I decided to leave it as the payoff vs. the inconvenience of blocking/unblocking different countries on request for both myself and the client, wasn’t worth it.

If this were the bank’s primary marketing site, I would absolutely have employed GeoIP restrictions.

This can be accomplished in a couple of different ways. At the server level, I could use the GeoIP module, or I can use one of the free Cloudflare firewall rules and block access to all but the countries I specify.

For most countries, this will stop DDoS attacks immediately, but you may be out of luck if the bulk of the attack is originating from your own country.

### Cloudflare DDoS Protection

This is one of my favorite things about Cloudflare. If my websites come under attack, I can flip a switch inside my Cloudflare account and turn on “I’m under attack” mode. If all else fails, this option would be my final stand.

“Cloudflare Under Attack Mode performs additional security checks to help mitigate Layer 7 DDoS attacks. Validated users access your website, and suspicious traffic is blocked. When enabled, visitors see an interstitial page… The “Checking your browser before accessing…” challenge determines whether to block or allow a visitor within 5 seconds.

SOURCE: https://support.cloudflare.com/hc/en-us/articles/200170076-Understanding-Cloudflare-Under-Attack-mode-advanced-DDOS-protection-

It’s not perfect for website visitors, but it’s far better than the alternative, and it’s a legitimately awesome, 100% free service that you can easily implement on any of your websites.

Further reading: https://blog.cloudflare.com/introducing-im-under-attack-mode/

 

## Part 6. Preventing Injection and Cross-Site Scripting (XSS) Attacks

Next up is blocking injection attacks that aim to compromise a site with malware and/or send malicious code to website visitors.

These are the type of attacks that most people imagine when we talk about malware and the type of attacks we all dread. They’re terrible for our visitors, terrible for our reputation and SEO, and they’re a HUGE PIA to clean up. 10,000 websites get blacklisted by Google every single day because of these types of hacks. If your website gets blacklisted, you can say goodbye to 95% of your organic traffic.

### Web Application Firewall (WAF)

A good WAF enhances every aspect of your website’s security, including everything we’ve already discussed.

GridPane comes with 3 Web Application Firewall integrations:

6G and 7G are great for most small business websites, and 7G is my WAF of choice for all my other websites. They do a great job, and they’re lightweight, and 7G even allows you to add your own custom rules.

ModSecurity is a sophisticated enterprise-level firewall, and this is what I’m using on these two sites. On GridPane, it comes pre-configured with the full OWASP foundation 3+ Core Ruleset (CRS) and is set to paranoia level 1 as the default.

I’ve set the paranoia level to #2 (of 4, 4 being the most strict), and the anomaly threshold is the default 10. ModSecurity is an entire topic in itself, just know that this is pushing the boundaries of extreme for these sites.

If you’re a GridPane client, you activate ModSec inside your account by opening up your customizer > Security tab and clicking through to Modsec.

### What does ModSecurity do?

ModSecurity is configured to protect sites from a wide array of attack vectors, including:

#### ModSecurity and Performance

ModSecurity is more resource-hungry than the 6G and 7G WAFs. This is due to the more comprehensive nature of how it detects patterns of bad behavior. It’s probably overkill, to be honest, but as server resources aren’t a concern for this project, it’s another good reason to go with the best option available to me. The websites are also extremely simple, so unlike more complex websites where significant fine-tuning can be necessary, this wasn’t a concern.

Note: For most websites, 7G is what we’d recommend and what I use for all other websites that I manage.

The server is more than capable, and the maximum concurrent visitors will be at most 10-20 at the same time, no dynamic requests (all cache, no PHP or MySQL processing), and our stack is extremely efficient. This server will never come close to being remotely stressed unless it gets DDoS’d, and in that case, I’ll be flipping on Cloudflare’s “I’m under attack” mode and employing GeoIP restrictions.

### Block wp-trackbacks.php

WordPress has a built-in mechanism to allow trackbacks (notifications on your posts that someone has linked to them). Unfortunately, trackbacks have, in the past, led to several MySQL injection vulnerabilities and, if unguarded, can lead to a lot of spam.

They’re also annoying. I’ve blocked them.

### Disable PHP execution in the uploads, plugin, and theme directories

The uploads, plugins, and theme directories each need to be writable for your website to function properly. Your theme and plugins need their directories to be writable to upload and update, and your uploads folder needs to be writable so that you and other users can upload files to your website.

The problem here is that while this is a necessity for your site, it means that hackers can exploit these directories by uploading malware to them. If this happens, and your directories also allow for PHP execution, then this malware can be executed and infect your site and potentially your entire system if your server isn’t properly isolating each website.

Disabling PHP execution won’t prevent hackers from being able to inject PHP malware if your site has a vulnerability through either WordPress core or a theme or plugin. However, it does mean that this malware won’t be able to execute once injected.

This is a major step towards preventing one of the most common types of security vulnerabilities, especially as plugin vulnerabilities are the leading cause of WordPress hacks.

Disabling PHP execution should be a part of your security setup, and if you do have a plugin or theme that requires it, it may be worth contacting that plugins author and/or looking for an alternative solution.

GridPane automatically blocks requests to maliciously uploaded PHP files in the WordPress uploads and themes directories. We don’t do this in the plugins directory by default as some plugins require this to function correctly (which we highly disapprove of, by the way…), but this is a simple task (especially on GridPane as it’s just clicking a toggle) and I’ve disabled PHP execution here as well.

Depending on your server configuration, you may need to either edit your .htaccess file (Apache and OpenLiteSpeed), or add a deny directive in Nginx, or just use a plugin – most security plugins have this feature.

### Security headers

All GridPane websites are launched with security headers in place to ensure security vulnerabilities such as cross-site scripting and clickjacking are automatically prevented. This shuts down one of the biggest security vulnerabilities on all websites online today, WordPress or not.

I’ve also implemented a Content Security Policy (CSP). More on this in part 7.

### Cloudflare DNS Firewall Rules

Cloudflare comes with some great features that can be enabled by turning on the orange clouds in the DNS page of your account. This includes some cool default firewall options as well as an extra 5 free custom firewall rules.

My Cloudflare firewall settings are as follows:

Medium Security “challenges both moderate threat visitors and the most threatening visitors”.

Bot Fight Mode “challenges requests matching patterns of known bots before they can access your site.”

The Browser Integrity Check looks for HTTP headers commonly abused by spammers and challenges visitors without a user agent (or non-standard user agents) to block abusive bot traffic.

###### 2023/2024 Update

Today, I would employ all the firewall rules detailed in parts 2, 3, and 4 of this article:

Cloudflare Firewall Rules for Securing WordPress Websites

 

 

### GridPane Additional Security Measures Tab

If you're a GridPane client, the bulk of the hardening options discussed in parts 3, 5 and 6, can be easily activated by simply clicking a toggle inside your websites customizer > Security tab:

## Part 7. Content-Security-Policy (CSP)

A Content Security Policy (CSP) is a set of instructions for browsers to follow when loading up your website, delivered as part of your website’s HTTP Response Header.

This is a widely supported security standard that can help you prevent injection-based attacks by fine-tuning what resources a browser is allowed to load on your website.

It specifies exactly where the browser is allowed to load resources from, and it’s an effective way of blocking anything malicious loading from elsewhere should instructions to do so somehow make their way into your website.

While there’s now already a lot of protection in place to prevent Cross-site Scripting (XSS), the single most effective way to stop this type of attack is with a Content Security Policy (CSP).

A browser simply does what it’s told and has no idea whether a script is malicious in nature or not. Implementing a CSP allows you to set rules for exactly where things like JS, CSS, fonts, or pretty much anything at all, are and aren’t allowed to load from.

GridPane makes it easy to activate a default CSP with GP-CLI. You can run a single command to create a CSP configuration file and then edit it as per your needs. Creating an effective and secure CSP is no simple task, though. It’s important to take the time to learn what they do, how they work, and then thoroughly test them in a staging environment to ensure that you don’t accidentally break your live websites.

This is another big topic in its own right. If you’d like to begin learning more, please check out our Knowledge Base article here for an introduction:

How to create a Content Security Policy (CSP Header)

 

## Part 8. Security Monitoring

When it comes to keeping a website secure, there’s not much any security plugin can offer at this point with everything that’s already now in place. Most of what these plugins do is essentially a band-aid for insecure web hosting.

However, there are still a couple of things that I personally wanted to implement, which some security plugins can assist with. These were:

###### 2023/2024 Update

Below details what I employed at the time with Sucuri, and it’s still not a bad setup. Today, I would just install Patchstack’s free plugin and have it email me alerts if any plugin vulnerabilities are found.

### Sucuri (The Free Version)

For this, I choose the free Sucuri plugin, and while it doesn’t really provide any additional protection, it acts as my website monitoring tool, which is still a valuable addition. It also takes just 2-3 minutes to set up.

Sucuri’s SiteCheck malware scanning feature is an external tool, so its scope is limited (it can’t do any server-side scanning), but it will at least let me know if any malware were to show up on the front end of either website.

Sucuri SiteCheck, scans for:

The core integrity checks will also alert me if any WordPress core files are modified, which is a pretty firm indication of a hack, and will allow me to check those files.

Sucuri also keeps me informed via email of specific security-related events. I’ve adjusted my settings to receive email alerts for:

That all keeps me pretty well informed and lets me know if anything requires my attention.

I should note here that on its own, the free Sucuri plugin is extremely limited and doesn’t do enough to keep the average website safe. If you wanted to use it for more than just a variation of the above, you would need at least their $200/year per site plan for legitimate protection.

### Maldet and ClamAV Malware Scanning

GridPane Developer accounts include access to Maldet and ClamAV. This software scans servers looking for signatures of thousands of instances of known malware and then logs the results as mini-reports.

It’s not a malware cleaner, but it is a very handy tool for the security toolbox if you’re a GridPane client.

Our integration sends out Slack notifications with details of these scans, and these take place once a day.

If you’d like to learn more about Maldet and ClamAV, check out our Knowledge Base article here:

An Introduction to Maldet and ClamAV Malware Scanning

### Better Uptime

I monitor the uptime of all the websites I manage using Better Uptime. Any uptime monitoring tool will do, but if either of these websites goes offline for more than 3 minutes, I’ll be alerted and then can begin to deal with whatever the problem is, be it security or otherwise.

Whatever the reason, website downtime is going to be displeasing to clients, so this is important for your business in general. The reason I’m using Better Uptime is simply because they had a great deal on AppSumo. I’ve been very satisfied with their service thus far, but there are plenty of decent tools to get the job done.

 

## Part 9. Emergency Action Plan

### Backups, Backups, and More Backups

To quote Patrick, our CEO: “Good backups are like insurance… if insurance covered everything, cost practically nothing, and always paid out. They are the single most cost-effective investment in your online presence that you will ever make.”

I couldn’t agree more. I’ve seen too many situations where simply having just 1 available backup would have saved someone’s ass. But alas, having zero backups appears to be far more common than having even just 1.

I back these websites up at:

If anything were to happen to these websites – either my editor colleague accidentally deleted all the content or the server was corrupted at the data center (extremely rare), or whatever the case may be – I can easily temporarily suspend the site, then get them live again in 15 minutes or less once I’m aware there’s an issue. Good as new.

### Additional Measures

If there was a security issue, I’d also immediately update everything that needs updating, remove all accounts except for my own, and I’d probably also install the free version of MalCare and have the sites thoroughly scanned by their free service, and maybe even Wordfence too (removing them afterward). Then I’d take things from there.

 

## Part 10. Launch and Maintain

Security is never “done”.

According to Sucuri, In 2019, 56% of hacked websites were outdated at the point of infection.

Once live, basic maintenance is required to keep these websites secure. All that means is regular WordPress core, theme, and plugin updates. For most of the clients I still personally host I do this around once every 2 weeks. For these two websites, I run updates at least once per week. As simple as this is, it’s one of the most effective ways to keep your websites secure.

 

## Final Thoughts

There’s always more than can be done, such as:

These may be useful depending on your hosting and security setup, and the type of sites you manage. Or they may be overkill.

### Security Plugins

All of the typical security “suite” plugins that most people think about when we talk about security plugins have their pros and cons. My thoughts on this topic changed over the course of 2022. I would recommend you thoroughly research any security plugin

To answer the real question you may be wondering about…

 

 

### Does GridPane recommend a specific security plugin?

We get asked this a lot. In short, we recommend the plugins talked about in this article:

Fortress
WP Fail2Ban
Patchstack

### Perfect Security Does Not Exist

Due to the ever-changing nature of WordPress (and all CMS platforms), the code base of our websites regularly changes, and it’s just not possible to guarantee 100% protection.

I can implement a comprehensive security strategy and use good judgment when choosing themes and plugins, but I can’t prevent a hack from occurring via something I can’t foresee or control, such as a zero-day vulnerability in a plugin that has previously had a stellar track record.

Fortunately, these things are rare, and implementing all of the security measures outlined in this article, plus choosing themes and plugins from reputable developers (who I trust will fix issues swiftly and competently should they arise) and that are actively maintained, will help us mitigate the damage that most of these types of potential vulnerabilities can cause.

#### That’s all, Folks!

This details every step I’ve taken to secure these two WordPress websites, along with a few extra considerations. I hope you’ll find it to be a valuable roadmap for securing your own websites.

 

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

### One comment

## Leave a ReplyCancel Reply

Your email address will not be published. Required fields are marked *

Name  *

Email  *

Website

Please check the box below to consent to the processing of the submitted personal data in accordance with our Privacy Policy, including the transfer of data to the United States.

I have read and accepted the Privacy Policy
		 *

Add Comment *

Post Comment

 

 