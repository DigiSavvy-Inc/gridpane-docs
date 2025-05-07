# Default GridPane Security and Additional Options | GridPane

# Default GridPane Security and Additional Options

 

5 min read 

### Table of Contents

 

## Introduction

GridPane takes care of a significant part of the general security for your websites out of the box, and locks down your servers during the provisioning process.

This does not mean your websites are invulnerable, and developing good security practices (and perhaps even helping your own clients implement), is still a requirement when locking down your websites.

It is, however, handy to know exactly what we do take care of so that you don’t need to worry about it, and can create your own process / checklist that you can follow each time you set up a new website on GridPane.

 

## GridPane Server Hardening

###### 1. SSH lockdown

The root user is locked down to secure SSH access only.

###### 2. Linux UFW configuration

The Linux Uncomplicated Firewall is configured out of the box during the server provisioning process.

###### 3. Fail2Ban preconfigured

Fail2Ban is an intrusion prevention software framework that’s highly effective at preventing brute-force attacks. It is enabled on all GridPane servers out of the box and is protecting the SSH port.

###### 4. System user isolation

New system users created via our platform are completely isolated and secure from one another, with only the necessary privileges applied.

###### 5. Auth and Fail2Ban logs preconfigured

The auth log is responsible for logging all authentication-related events. You can use this log to view failed login attempts, identify brute force attacks, or anything related to suspicious authentication attempts.

The Fail2Ban log logs all Fail2Ban-related events and records IPs that have been banned/unbanned.

###### 6. Security updates/patches

GridPane takes care of all necessary server updates. This includes all security-related updates, security patches, and keeping our server stack and platform up-to-date. Learn more here:

Server Updates / Maintenance / Security Patches – What Updates Does GridPane Take Care Of?

###### 7. /tmp Lockdown (Ubuntu 22.04 and future Ubuntu releases only)

The /tmp directory is mounted as noexec. This means that this directory cannot contain executable binaries (and ensures that system users cannot execute code from the /tmp directory).

 

## GridPane’s Default WordPress Security

###### 1. Secure PHP version by default

New websites will always be provisioned on an up-to-date version of PHP – unless you go out of your way and manually make it otherwise.

###### 2. Secure usernames and passwords by default

You also have the ability to set your own default username and password.Also please note that if you import a website that overwrites the database, this also overwrites the default username and password.

###### 3. We install the latest version of WordPress on new site builds

No unpatched security vulnerabilities in out of date versions.

###### 4. Disable directory browsing / System file protection

Prevent anyone from seeing your WordPress files and prevent access to readme.html, readme.txt, install.php, and wp-includes.

###### 5. Disable PHP execution in the uploads and themes directories

Automatically block requests to maliciously uploaded PHP files in your WordPress directories.

###### 6. Secure wp-config.php

We store the wp-config.php file one level up from the htdocs directory. Your wp-config.php file contains your database username and password along with other information about your website. We keep your wp-config hidden and protected.

###### 7. Security headers

We implement security headers by default to ensure security vulnerabilities such as cross-site scripting and clickjacking are automatically prevented. This shuts down one of the biggest security vulnerabilities on all websites online today, WordPress or not.

###### 8. SFTP and SSH access only

We enforce secure server connections. No exceptions.

###### 9. Server-level rate limiting

Out of the box we limit requests to wp-login.php to 1 hit per second to protect against brute force attacks. We also implement a slightly less strict rate limit on the admin-ajax endpoint.

 

## Additional WordPress Security Options

Above are the things we do by default. This section details additional options that you can configure on an as-needed basis, and are completely customizable to your specific needs.

###### 1. Web Application Firewall (WAF) options

We have deep, customizable integrations with the 7G WAF and ModSecurity. These allow you to implement a WAF at the server level to protect your websites against a variety of malicious URI requests, bad bots, spam referrers, and more. It only protects your website, but it will help reduce your server’s resource consumption. Learn more here:

###### 2. Website isolation through System Users

Assigning each of your websites to a unique system user will keep them completely isolated from one another. If a site was ever compromised, it will be unable to infect any other websites if it’s on its own system user. At the time of writing, system users are optional, but in the future they may be mandatory. Learn more here:

Change the Site Owner (System User) of a GridPane Site

###### 3. WPFail2Ban integration

We have handy CLI integration with Fail2Ban on the server level to implement brute force protection, and also with the wpFail2Ban plugin on a site by site basis. This will allow you to implement a variety of different security options to keep the bad guys off your server.

Configuring Fail2Ban to Prevent Brute Force Attacks

###### 4. Disable XML RPC

XML RPC is an old, outdated, and insecure method of remotely posting to your WordPress website. If you’re not using it, you should disable it completely. Check out the beginning of the Fail2Ban article above or the Nginx hardening article below for instructions – it’s quick and easy.

###### 5. Server-level WordPress hardening measures

GridPane allows you to configure individual websites on an as-needed basis to easily increase their security. This includes blocking XML-RPC, load-scripts.php, blocking PHP executing in wp-content, block comments, block links opml, block trackbacks, and block the wp-admin upgrade and install file. Learn more here:

Additional Security Measures: WordPress Website Hardening for Nginx and OpenLiteSpeed (OLS)

###### 6. Content Security Policy (CSP)

GridPane makes it easy to activate a CSP with GP-CLI. You can run a single command to create a CSP configuration file, and then edit it as per your needs. Learn more here:

How to create a Content Security Policy (CSP Header)

###### 7. A+ Grade SSL certificates

Exactly what it says on the tin. We can’t force SSL’s, but you should always use them.

 

## Fortress Security Plugin Integration

Fortress is the only WordPress security plugin that we officially recommend and provides real-world protection for your site in the areas that can only be effectively handled at the plugin level. GridPane offers a complete, server-level integration. Learn more here:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

