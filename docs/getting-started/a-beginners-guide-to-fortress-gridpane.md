# A Beginners Guide to Fortress | GridPane

# A Beginners Guide to Fortress

 

10 min read 

### Table of Contents

 

## Introduction

Snicco, the team behind the Fortress Security plugin, are an enterprise WordPress development team and independent security research firm that quickly gained attention in the space by researching and fixing vulnerabilities in other WordPress security plugins.

Based on their research, they created Fortress to address the real-world threats facing the WordPress ecosystem. This guide offers an overview of these threats and how Fortress protects against them.

This guide also serves as a simplified version of our Fortress Part 1 article:Fortress Security Part 1: How Fortress Secures WordPress

 

## About Fortress

To implement the most important aspects of WordPress security, there needs to be a hosting-level connection, and Fortress has been designed and built with a direct hosting integration in mind.

The core idea behind hosting partnerships is only to include what can be done effectively at the plugin level and nothing more. You get EVERYTHING that can be hardened effectively in PHP and NONE of the things that are useless at best and resource hogs at worst.

Unlike other security plugins, Fortress is NOT built for the lowest common denominator, which means there are no security compromises by trying to accommodate every hosting environment and outdated PHP.

For example, the reason every other security plugin stores encryption keys in the database is because it’s the only thing they can rely on being available. Fortress doesn’t suffer from these limitations.

### Fortress Modules

Fortress consists of the following modules that you can use independently of each other:

Modules 1-4 and 6 are activated by default, and together they harden your security at every step of your website’s authentication lifecycle. Vaults and Pillars can be manually configured on an as needed basis.

### Admin Takeover Protection

While Fortress protects against a wide array of attacks, vulnerabilities that allow administrator-level takeover of a WordPress website are the most severe in terms of WordPress security and are worthy of note.

The 3 most common ways this occurs are through:

Thomas Raef of WeWatchYourWebsite shared data gathered from millions of WordPress sites that showed that 67% of all WordPress compromises in 2023 were caused by 1 and 2:

The Real Attack Vector Responsible for 60% of Hacked WordPress Sites in 2023

Serious vulnerabilities in overwhelmingly popular plugins such as Elementor have allowed hackers to take advantage of number 3.

Fortress offers in-depth protection against all of these attacks.

 

## Secure Two-Factor Authentication

One of the biggest problems with many security plugins (both now and in the past) is that their two-factor authentication is not only NOT secure, but its activation may also have led to your website being hacked in certain circumstances. Snicco provided numerous plugin vendors with the code needed to fix such issues.

In Fortress, two-factor authentication employs the most up-to-date, best security practices.

### 2FA Rate Limiting

Fortress is the ONLY security plugin that rate-limits failed 2FA attempts. Without this, 2FA can be brute forced, simple as that.

If the rate-limiting threshold is exceeded, Fortress will “lock” the user account, which means:

 

## Password Security

The Fortress password security features significantly upgrade the base WordPress password security and enforce a strong password policy (which should ALWAYS be a priority and is a necessary part of security practices such as PCI compliance).

 

### Secure Password Hashing

Fortress replaces the outdated WordPress md5-based password-hashing functions with its own implementation based on the libsodium core PHP extension, which is the best cryptography implementation in PHP.

Encryption keys are stored securely on the server, not the database.

 

### Strong Password Policy

Weak passwords are a legitimate threat to your website security. Fortress enforces a strong password policy for all user accounts, which means that weak passwords are not allowed. No exceptions.

Passwords can be between 12 and 4096 characters and must score at least a 3 out of 4 according to the zxcvbn password entropy estimator.

 

### Disabling password resets for privileged users

Recovering a forgotten password is a balance between security and convenience. Fortress uses an opt-in approach for password resets to enhance security.

By default, administrator and editor users cannot request a password reset link or reset passwords on their profile page. This can be modified to your requirements, including adding or excluding different user roles.

 

### Disable application passwords

WordPress allows for passwords that applications (not humans) can use to access the site.

The problem is that, while safe in theory, WordPress application passwords are vulnerable to social engineering attacks where an attacker tricks an unsuspected site admin into adding a new application password by clicking on a link.

Most websites don’t require them, and unless they do, they should be turned off.

 

### Decrease password reset link duration

By default, WordPress password reset links are valid for 24 hours which is unnecessarily long. Fortress decreases this duration to 30 minutes.

 

## Rate Limiting

Rate limiting is a way to control how often requests are made to a website. This helps prevent the site from being overloaded or attacked by hackers who try to flood it with too many requests.

When too many requests are made in a short time, rate limiting blocks further attempts until a later time. It’s commonly used to protect against denial-of-service attacks and to reduce the impact of bots.

Rate limiting helps keep your website stable and secure by managing the number of requests it receives. However, many WordPress security plugins can only protect against attacks from a single IP address, which isn’t enough in today’s world.

The Fortress plugin offers two rate-limiting features: Password reset throttling and Login throttling. It uses a modern rate-limiting method called the “Token Bucket” algorithm, which is more efficient because it stores less data and uses the WP Object Cache instead of the database.

 

### Password Reset Throttling

The purpose of password reset throttling is to prevent attackers from flooding a user’s email inbox with password reset requests and can be used to abuse SMTP services.

Fortress limits password resets to once every 15 minutes per IP address.

 

### Login Throttling

Login throttling is a rate-limiting mechanism that restricts the number of login attempts from various dimensions to protect against different attack vectors.

Fortress employs sophisticated login throttling through 4 different methods that provide advanced protection while simultaneously protecting real users.

 

## Secure Sessions

A session in WordPress refers to the period of time when a user is logged in to the website. When a user logs in, WordPress creates a session for that user, and as long as the session is active, the user can access protected pages and perform actions that require authentication.

The session is maintained by using a session cookie, which is a small file stored on the user’s browser. This cookie contains a unique identifier that allows WordPress to associate the user’s browser with their session.

Fortress makes WordPress sessions far more secure.

 

### Session management and security

Stolen cookies are one of the most common ways WordPress websites are compromised. Here’s the problem in a nutshell:

At the time of writing, the Linus Tech Tips YouTube channel had just suffered a similar attack – detailed video here.

Fortress uses four dimensions (timeouts) to harden WordPress session security. These protect user sessions from being exploited if their session token is stolen, and even helps protect your account from unauthorized access if you’ve left your computer unattended or used a public computer OR if a machine is shared between multiple people using the site with different accounts.

 

 

### Important

Many many viruses are built for the sole purpose of cookie harvesting. This is a huge security problem, and no one in the WordPress security world even tries to protect against this.

### Fortress Sudo Mode

Fortress has a feature called sudo mode that gives a user elevated privileges for a certain period after they log in. This is similar to the Linux sudo command. After the time is up, the user’s privileges go back to normal.

During sudo mode, the user can use the website normally. If they are not in sudo mode and try to access a protected page, Fortress will ask them to confirm their password.

This is a feature that companies like Amazon use to let you remain logged in and add items to your basket, but also make you re-authenticate when doing anything billing related.

 

## Vaults & Pillars

Vaults & Pillars are a game changer for WordPress security, allowing you to encrypt sensitive data and protect your site from malicious settings changes.

 

 

### Recommended Reading

I highly recommend checking out Snicco's introductory blog post here:
Solving WordPress’s Pathological Plaintext Problem: Introducing Fortress Vaults&Pillars

### Vaults

Fortress Vaults tackles one of the most significant potential security vulnerabilities: Storing sensitive data in plaintext within the WordPress database.

This, unfortunately, is such a common practice that almost every single WordPress theme or plugin developer defaults to storing sensitive data in plaintext in the database without any consideration for the possible ramifications. This is because (a) they’re not thinking about SQLi vulnerabilities, and/or (b) SQLi vulnerabilities are not considered to be their problem.

After all, if none of the popular WordPress security plugins consider them as a part of their threat model, why would they?

Even just a read (not even a write) SQLi vulnerability presents a serious threat. For example:

The ramifications of these breaches are not just theoretical. These happen every day and can cause significant harm to businesses and individuals alike (like the $70,000 Stripe hack you may have heard about).

Any information that’s sensitive and is currently stored as plaintext in the wp_options table can and should be stored in a Vault.

 

### Pillars

Pillars can be used to handle important settings and options in the wp_options table securely. These settings do not necessarily pose a security threat if exposed, but they could be maliciously altered to negatively impact the security and stability of your website.

For example, some plugin/theme vulnerabilities could allow hackers to enable user registration on your website and set the default user role to administrator, allowing for a full site takeover.

Another example is SEO sabotage by blocking search engines from crawling your site, and changing permalinks so that content previously ranking in the search engines no longer appear.

These settings should never be accidentally modified in production and can be locked with Pillars, making it impossible for attackers to modify them.

 

## Code Freeze

Code Freeze gives you 80% of the benefits of an immutable deployment strategy without the need to manage your websites via our Git integration.

Code Freeze detects if your site is running in production and ensures that:

However, you can still update any existing plugin, theme, or core from within the admin dashboard and WP-CLI.

You can learn more about Code Freeze in Calvin’s launch post here: Fortress Code Freeze – Reap the Security Benefits of “Immutable WordPress” without the Complexity

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

