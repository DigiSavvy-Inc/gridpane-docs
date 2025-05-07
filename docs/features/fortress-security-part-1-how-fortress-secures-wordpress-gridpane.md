# Fortress Security Part 1: How Fortress Secures WordPress | GridPane

# Fortress Security Part 1: How Fortress Secures WordPress

 

21 min read 

### Table of Contents

 

## Introduction

Snicco, the team behind the Fortress Security plugin, are an enterprise WordPress development team and independent security research firm.

Through their research and guidance they have helped 24 of the most well-known security plugins patch vulnerabilities in their code – many extremely serious that could have led to a full site takeover. Their security research found DOS vulnerabilities, a complete lack/misunderstanding of encryption, and unjustifiable security shortcuts. Many plugins even copied code from others verbatim, introducing inherent security issues into their codebase, and every plugin evaluated had at least 1 vulnerability, with most having 3 or more.

Based on their research and the serious issues present in other solutions, they have created Fortress, a plugin that focuses on keeping WordPress locked down by significantly upgrading WordPresses own security practices, adding secure 2FA, rate limiting, more secure sessions, and forcing strong passwords with best available cryptography.

 

## About Fortress

### No Security Compromises

The core idea behind hosting partnerships is only to include what can be done effectively at the plugin level and nothing more. You get EVERYTHING that can be hardened effectively in PHP and NONE of the things that are useless at best and resource hogs at worst.

Unlike other security plugins, Fortress is NOT built for the lowest common denominator, which means there are no security compromises by:

### Fortress Modules

Fortress consists of the following modules that you can use independently of each other:

The first four modules are activated by default, and together they harden your security at every step of your website’s authentication lifecycle. Vaults and Pillars can be manually configured on an as needed basis.

### Quality Assurance

Fortress undergoes rigorous quality assurance testing to ensure every code base change works. This includes 1200 automated tests before every single release across all combinations of supported WordPress and PHP versions.

### WP-CLI Configuration

Fortress is built with a CLI-first approach and has full feature parity between the Web UI and the WP-CLI.

To improve the developer experience and reliability of the default WP-CLI, Snicco have created their own open-source BetterWPCLI library, and this is used everywhere in Fortress.

### Customization

All of the modules in Fortress are highly customizable and can be configured per user role. Even the most complex scenarios can be accommodated.

 

## Default Settings and Workflow

Everything in Fortress is configurable, so if there’s a default setting that you wish to change (or make recommendations about to your clients) it’s all flexible. That all said, these are the 3 things that may change the workflow of your clients and/or team members with the default settings:

 

## Secure Two-Factor Authentication

One of the biggest problems with many security plugins (both now and in the past) is that their two-factor authentication is not only NOT secure, but its activation may also have led to your website being hacked in certain circumstances. Snicco provided numerous plugin vendors with the code needed to fix such issues.

In Fortress, two-factor authentication employs the most up-to-date, best security practices, can be enforced at a granular level, and has its own WP-CLI.

### 2FA Rate Limiting

Fortress is the ONLY security plugin that rate-limits failed 2FA attempts. Without implementing rate-limiting, 2FA can be brute forced, simple as that.

By default, Fortress allows five failed 2FA attempts (configurable). The failed attempts counter is reset after a successful 2FA login.

If the rate-limiting threshold is exceeded, Fortress will “lock” the user account, which means:

### Compatibility

 

## Password Security

The Fortress password security features are broken down as follows:

We’ll look at each of these below.

 

### Secure Password Hashing

WordPress uses an outdated md5-based hashing scheme for password security that is no longer considered secure. Fortress solves for this.

 

### Password Policy

Fortress enforces a NO-BS password policy for all user accounts, which means:

*The disable emoji GridPane additional security hardening measure does not interfere with password setting.

 

 

### Additional Note

The zxcvbn estimator is a password strength estimator created by Dropbox inspired by password crackers that weighs 30k common passwords, common names, and surnames according to US census data, popular English words from Wikipedia and US television and movies, and other common patterns like dates, repeats, sequences, keyboard patterns, and l33t/1337 speak.

### Disabling password resets for privileged users

Recovering a forgotten password is a balance between security and convenience. Fortress uses an opt-in approach for password resets to enhance security.

A user with any of the roles defined in the password_policy_excluded_roles option will not be able to:

By default, this applies to users of the roles:

Passwords can always be reset using WP-CLI.

 

 

### Edge Cases

some plugins like WooCommerce and LMS have their own mechanisms to reset passwords without using the allow_password_reset hook. In such cases, Fortress cannot prevent password resets, and you may need to contact the plugin vendor to add the hook or inspect the code and fire it yourself at the appropriate time. More info on this can be found in part 2 of this series.

### Disable application passwords

The problem: WordPress application passwords are vulnerable to social engineering attacks, where an attacker can trick an unsuspected site admin into adding a new application password by clicking on a link.

WooCommerce + Zapier are a common combination that require this functionality, so on these sites it will need to turned back on.

 

### Decrease password reset link duration

By default, WordPress password reset links are valid for 24 hours. Fortress decreases this duration to 30 minutes.

This can be adjusted if 30 minutes is too strict for your use case but is plenty of time for most websites.

 

### Destroy all user sessions on password change

The Problem: WordPress invalidates a user’s sessions after a password change by coincidence because a user’s password hash happens to be part of his authentication cookie. To be precise, the 8th – 12th characters of the password hash are part of a user’s auth cookie. However, the difference between the 8th – 12th hash characters is not guaranteed, making this unreliable.

For this reason, Fortress explicitly destroys a user’s sessions after he changes his password.

 

## Rate Limiting

Rate limiting is a technique used to control the rate at which requests are made to a system or service to prevent overload and to protect against malicious attacks, such as brute-force attacks, that attempt to flood a system with too many requests.

When the rate limit is reached, further requests are blocked until a later time. It is commonly used in web applications to prevent denial-of-service attacks and to limit the impact of automated bots.

Rate limiting is an important technique used to maintain the stability and security of your website by controlling the rate of requests that it receives. However, most WordPress security plugins can only protect against attacks from a single IP because they still operate with the 2000s mindset of “one attacker = one IP.” This could not be further from the truth in 2023.

Fortress includes two rate-limiting features: Password reset throttling and Login throttling and has implemented a novel (in WordPress) rate-limiting algorithm (Token Bucket) that, instead of storing all failed attempts, only needs to store a counter per IP/username/etc. This results in far less storage and uses the WP Object Cache directly instead of the database.

 

### Password Reset Throttling

 

### Login Throttling

Login throttling is a rate-limiting mechanism that restricts the number of login attempts from various dimensions to protect against different attack vectors.

 

## Secure Sessions

Before diving into each of the features below, it’s important to understand what a session is and how it relates to your website’s security. Here’s a quick breakdown:

Fortress makes WordPress sessions far more secure.

 

### Custom user session storage

WordPress uses a custom session implementation that stores arbitrary data (the session) in the wp_usermeta table. This has some disadvantages:

Fortress solves for all of these issues with its own custom user sessions.

 

### Session management and security

###### The Problem

At the time of writing, the Linus Tech Tips YouTube channel had just suffered a similar attack – detailed video here.

 

 

### Important

Many many viruses are built for the sole purpose of cookie harvesting. This is a huge security problem, and no one in the WordPress security world even tries to protect against this.

###### The Solution

Fortress uses four dimensions (timeouts) to harden WordPress session security. Each of these is explained below. Configuration options are available to overwrite default values.

###### 1. The Absolute Timeout

###### 2. The Rotation Timeout

This means that if an attacker or a virus on the local machine steals a token, they have a limited amount of time (the rotation timeout period) to use it before it becomes invalid. If a user continues to use the site after the token has been stolen, they will receive a new token, and the old one will become invalid.

However, if an attacker immediately starts exploiting the stolen token, there is a race condition between them and the legitimate user.  Once the rotation timeout is exceeded, the contents of the current user session are copied to a newly generated session token (auth-cookie). The first incoming client request with a valid auth cookie will receive the new auth cookie.

This means that either the legitimate user or the attacker could win and the other party will be locked out after the new auth cookie. This is a serious problem, and so shorter the window, the more secure your session is.

###### 3. The Idle Timeout

###### 4. The Sudo Mode Timeout

This complements the absolute timeout and idle timeout to provide better security.

 

### Fortress Sudo Mode

 

## Vaults & Pillars

Snicco continue to lead the charge for a safer and more secure WordPress ecosystem. Vaults & Pillars are a game changer in this record, tackling one of the biggest potential security vulnerabilities: Storing sensitive data in plaintext within the WordPress database.

 

 

### Recommended Reading

I highly recommend checking out Snicco's introductory blog post here:
Solving WordPress’s Pathological Plaintext Problem: Introducing Fortress Vaults&Pillars

This, unfortunately, is such common practice that almost every single WordPress theme or plugin developer defaults to storing sensitive data in plaintext in the database without any consideration for the possible ramifications. This is because (a) they’re not thinking about SQLi vulnerabilities, and/or (b) SQLi vulnerabilities are not considered to be their problem.

After all, if none of the popular WordPress security plugins consider them as a part of their threat model, why would they?

Even just a read (not even a write) SQLi vulnerability presents a serious threat. For example:

The ramifications of these breaches are not just theoretical. These happen every day and can cause significant harm to businesses and individuals alike (like the $70,000 Stripe hack you may have heard about).

The Fortress Vaults & Pillars (VnP) module allows you to address this critical problem by introducing an encryption layer for sensitive data stored in the WordPress database.

Fortress acts as a hidden translation layer between WordPress and the database, which means that all functionality of the WordPress Option API continues to work as expected without any code modification in WordPress Core or plugins.

 

### Vaults

A Fortress Vault secures a WordPress option (or a subset of it) by storing it encrypted in the wp_options table, allowing you to encrypt sensitive information that an attacker could exploit if they were to gain access to your database.

Examples of sensitive data include:

Any information that’s sensitive and is currently stored as plaintext in the wp_options table can and should be stored in a Vault.

 

### Pillars

Pillars can be used to securely handle important settings and options in the wp_options table. They are not necessarily settings that pose a security threat if exposed, but they are settings that could be maliciously altered in ways that could negatively impact the security and stability of your website.

So what should be a Pillar?

###### 1. Security-Critical Configuration Flags

These are settings that significantly impact your website’s security, and they are typically settings that can be turned on or off.

Unfortunately, in WordPress, these are often stored in the database for convenience, which means these can potentially be exploited if any of your themes or plugins (or even WordPress core) have vulnerabilities.

Examples include:

Exploiting these settings could allow hackers to enable user registration on the front end of your website and set the default role to administrator, allowing for a full site takeover.

###### 2. Locking Options for Reliability, Integrity, and Stability

Pillars can help secure settings that, if altered, could disrupt the stable operation of your WordPress website. They’re often simple strings or boolean values that shouldn’t be changed in a production environment – whether maliciously or out of user ignorance.

Examples include:

These settings should never be accidentally modified in production.

 

## Code Freeze

Vulnerabilities that allow administrator-level takeover of a WordPress website are the most severe in terms of WordPress security.

The 3 most common ways this occurs are through:

Thomas Raef of WeWatchYourWebsite shared data gathered from millions of WordPress sites that showed that 67% of all WordPress compromises in 2023 were caused by 1 and 2:

The Real Attack Vector Responsible for 60% of Hacked WordPress Sites in 2023

Serious vulnerabilities in overwhelmingly popular plugins such as Elementor have allowed hackers to take advantage of number 3.

### Code Lockdown

Code Freeze gives you 80% of the benefits of an immutable deployment strategy without the need to manage your websites via our Git integration.

Code Freeze detects if your site is running in production and ensures that:

However, you can still update any existing plugin, theme, or core from within the admin dashboard and WP-CLI.

Code Freeze is fully integrated into GridPane, and this includes our staging site workflows. This means that production sites are locked down and staging sites are automatically “unlocked” without any manual configuration.

### Learn More About Code Freeze

You can learn more about Code Freeze in Calvin’s launch post here: Fortress Code Freeze – Reap the Security Benefits of “Immutable WordPress” without the Complexity

And the official Developer documentation here:Developer docs: The Fortress Code Freeze module

 

## Up Next: Part 2 Quick Start Configuration Guide

This is part 1 of a 2 part series of documentation. Click below to begin learning how to configure Fortress:

Fortress Security Part 2: Quick Start Configuration Guide

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

