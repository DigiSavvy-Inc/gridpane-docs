# Fortress Security | GridPane

 

 

# Fortress: The Only Security Plugin that GridPane Officially Recommends

 

Fortress provides real-world protection for your site in the areas that can only be effectively handled at the plugin level. GridPane offers a complete, server-level integration.

 

 

Introducing Snicco Fortress

 

## Unlock Enterprise-Grade WordPress Security Without Hiring A Full Infosec Team

 

 

#### Laser-focused security measures:

Fortress only targets security threats that can be most effectively handled at the plugin level, eliminating unnecessary bloat and resource drains.

 

#### Absolute security commitment:

Unlike other security plugins that sacrifice security for broad compatibility, Fortress is built exclusively for supported versions of PHP, unlocking cutting-edge cryptography and security functionality.

 

#### Unmatched defense-in-depth:

Fortress is the only security plugin for WordPress that anticipates the potential failure of other plugins and builds safeguards to protect you regardless.

 

## The State Of WordPress Security: A Peak Behind The Curtain.

While WordPress Core continues to make great strides, many recent advancements have focused on developing the Gutenberg editor, leaving security enhancements lagging behind.

With WordPress Core’s development priorities focused elsewhere, many third-party security plugins have emerged to fill this void.

But instead of providing meaningful solutions…

Vendors often prioritize “security” features that could be implemented way more efficiently at the server or network level (such as WAF, malware scanning, or malware removal).

In many cases, they may even push features that are mere security theater, with the sole purpose of looking good on marketing copy, all while consuming your CPU.

In the fall of 2022, the team behind Fortress conducted a short audit of almost all major security plugins, and the results were alarming.

 

Snicco identified and privately disclosed 57 vulnerabilities in 24 plugins, affecting over 16 million sites. Many of these vulnerabilities could have led to a complete site takeover.

 

Most of the issues stemmed from not respecting the most basic security principles – such as not trusting user input, not storing sensitive data in plaintext, and avoiding homemade cryptography – which is concerning.

Additionally, some vendors’ inadequate handling of reported issues led them to conclude that an alternative solution is desperately needed.

#### Enter Fortress.

 

## Put An End To Second-Guessing Your Site’s Security.

Don’t settle for checkbox security. Fortress provides real world protection your site in the areas most effectively handled at the plugin level, and is deeply integrated into the GridPane stack.

By exclusively supporting PHP 7.4, 8.0, and 8.1, Fortress taps into the full strength of libsodium, the most potent encryption library available in PHP.

 

 

#### Two-Factor Authentication

A 2FA suite with unique defense-in-depth measures, impervious even if your entire database is compromised.

 

#### Password Security

A drop-in, argon2-based password hashing schema that will have hackers gnashing their teeth for decades instead of cracking your password hashes in hours.

 

#### Login Protection

Fortress's custom rate-limit implementation stops even the nastiest distributed, multi-IP brute force attacks in their tracks without frustrating captchas.

 

#### Session Protection

Fortress brings Fortune 500-level session hijacking and cookie-theft protection to WordPress.

 

#### Vaults & Pillars

Never store sensitive data in plain text in the database again! Secure your data with Fortress Vaults, and secure important settings in the wp_options table with pillars.

 

#### Code Freeze

The next best thing to an immutable codebase. Add significant defense-in-depth against attackers who have gained access to an administrator (or similar) account through any means.

 

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1638'%20height='1638'%20viewBox='0%200%201638%201638'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2021/05/Patrick-Square.jpg)### The guys behind Snicco are hands down among the most skilled developers I've ever met, and we've worked with people in over 100 countries, helping power over 120K websites. These guys know their s*** cold. I can't wait to see what they come up with next, and I look forward to hanging from their coattails for years to come.

- Patrick Gallagher, CEO of GridPane

 

 

## Unlike Other WordPress Security Plugins, Fortress Does NOT:

 

 

#### Eat up RAM and CPU with ineffective malware scanning:

Malware scanning fundamentally cannot be performed reliably at the plugin level.

Don't let anybody tell you otherwise.

Ideally, it should be performed off-server or in a different process that malware cannot easily alter.

 

#### Tank your site's performance with a general purpose WAF:

A general-purpose WAF that checks for bad request parameters, SQL injection, or similar offenses is orders of magnitude faster and more effective at the web server level or CDN level. (All GridPane account holders can use the 7G WAF).

 

#### Give false confidence with automatic malware removal:

Automatic malware removal rarely works perfectly, much less if the malware can alter the source code of the malware removal plugin to evade detection

 

#### Entertain hackers by changing the WP database prefix:

While absolutely useless for security, changing the WP database prefix might amuse an attacker while they scrape your entire database in seconds using automated tools.

Finally, while monitoring vulnerable plugins is important, it’s also a solved problem. There’s no need for us to reinvent the wheel, and this service is freely available using laser-focused solutions like Patchstack or WPScan.

 

 

## Frustrate Attackers With Unparalleled Defense-in-Depth.

Have you ever stopped to think about how unique your WordPress site is?

With its own combinations of plugins, themes, versions, and configurations.

#### Bad news:

This also means that at some point, your site will most likely have a unique vulnerability caused by one or more components in combination.

Unfortunately, most security plugins overlook this reality.They naively assume that as long as they’re operating correctly in their isolated bubble, your site is secure.

But that’s a dangerous misconception, leaving your site’s security hanging by a thread. The moment another component contains a vulnerability, traditional security measures crumble to pieces.

Fortress anticipates the potential failure of other components and builds safeguards to protect you regardless.

#### In other words, Fortress is prepared for the worst:

For all we know, your entire database could be compromised, or a rogue plugin might enable unauthorized admin user creation.

Yet, with Fortress, you can rest easy knowing that attackers still won’t be able to authenticate on your site.

Barring a full server filesystem compromise, Fortress serves as your resilient last line of defense or at the very least, puts up a formidable fight to make your site a highly unappealing target.

 

 

## Enjoy Instant Protection

You shouldn’t be responsible for configuring a security plugin unless you’re a trained security professional. Other vendors who shift this burden onto you are doing you a disservice.

Fortunately, Fortress is different.

 

 

#### Truly set and forget:

We spent weeks building a rock-solid default configuration that works for 95% of use cases.

 

#### A 20-tab settings page? Nowhere to be found:

For that exceptional 5 % of use cases, we have the most comprehensive and detailed developer documentation allowing you to configure even the most complex scenarios using a straightforward config file.

 

#### No dreaded installation Wizard:

You install Fortress, setup 2FA, and forget that it exists.

 

## Maintain your hard-earned site speed

Among many others, Fortress uses the following techniques to serve its responses in only a couple dozen milliseconds so that you maintain your hard-earned site speed.

 

 

#### Exclusive use of custom database tables with carefully crafted indexes:

Fortress will never bloat or otherwise interact with shared database tables.

 

#### Zero database queries for plugin settings:

Fortress caches its entire configuration on disk resulting in fastly superior performance to plugins that bloat your wp_options table with "autoloaded" settings.

 

#### A completely lazy-loaded codebase:

The entire codebase of Fortress is lazy-loaded, and no code is run if not explicitly needed for the current request.

 

#### Zero frontend assets on Non-Fortress pages:

Fortress does not require any JS or CSS files to be loaded on your site.

 

## Truly Developer Friendly

Fortress is built with a WP-CLI first approach, and each new update undergoes 1200+ tests before its production release.

 

 

#### Fortress treats the WP-CLI as a first-class citizen:

Powered by BetterWPCLI, any action that Fortress can perform in the UI can also be performed from the CLI. Most WordPress plugins barely have a WP-CLI integration, let alone one that's useful. With Fortress you can streamline your site builds.

 

#### Unmatched QA pipeline:

We invested over three months building an unmatched QA pipeline so that you never have to worry about hitting the update button.

 

#### 1200+ automated tests:

No change of the Fortress codebase is released unless all 1200+ unit and browser tests pass with 100% code coverage for all supported PHP and WP versions. Including upcoming WP versions.

## Get Started with Fortress

 

 

This pricing is available to all paid GridPane account holders (including LTD account holders).

 

Huge savings! Regular pricing for Fortress will start at $49/month, and it will NOT include client distribution.

 

These licences allow for client distribution, which would normally require a custom Agency license directly with Snicco.

### 1 Website

 

$125/year

 

Licensing to run Fortress on 1 website.

New: GridPane branded version of Fortress + full White Label at rate that’s TBD.

 

### 10 Websites

 

$750/year

 

Licensing to run Fortress on 10 websites: $75/year/site

New: GridPane branded version of Fortress + full White Label at rate that’s TBD.

 

### 50 Websites

 

$1500/year

 

Licensing to run Fortress on 50 websites: $30/year/site

New: GridPane branded version of Fortress + full White Label at rate that’s TBD.

 

### 100 Websites

 

$2500/year

 

Licensing to run Fortress on 100 websites: $25/year/site

New: Unbranded version of Fortress + full White Label at a locked in rate of $2/site/year.

 

New: GridPane branded version of Fortress + full White Label at rate that’s TBD.

 

Buy now! 

Buy now! 

Buy now!

Buy now!

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='300'%20height='300'%20viewBox='0%200%20300%20300'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2021/03/30-Day-Money-Back-Guarantee.png)#### 30 Days Money Back Guarantee

If you're unhappy with your purchase, no worries. This offer comes with a 100% Money Back Guarantee if it’s requested within 30 days of purchase.

 

## FAQ

 

What does my Developer Plus account already include?

Your Developer Plus account includes 50 licenses for the Fortress plugin while your account subscription is active.

Any licenses purchased on this page will be in addition to those 50 licenses. For example, if you purchase another 50 through this promotion, your total will be 100 websites.

What kind of Support and updates are included?

Support and updates are included for 12 months (which will be extended another 12 months on renewal), assuming that you have an active account at GridPane. Fortress can run in other hosting environments but would be unsupported by the GridPane team or the Snicco team.

Support will initially start with the GridPane community forum, where our team and Calvin are both active. It will then be escalated for internal testing by our team where needed, and then passed over to Snicco if it requires their attention.

When is the renewal date?

The renewal date is one year from the date of purchase.

How does the activation and site licensing process work?

Snicco are currently in the process of setting up a central licensing server on AWS.

GridPane will handle all of the license-setting, and it’ll ultimately be a “Install Fortress on this site” button where everything works out of the box.

Is Fortress only a plugin, or is it at the server level at GridPaneP?

Fortress is written 100% in PHP and runs as a (must-use) plugin. Imagine it as a PHP program with a tiny WordPress layer on top.

Now the server part: You can significantly increase the security Fortress (or any other security plugin) gives you by having tight integration with the server stack where the plugin ultimately runs. This manifests in way too many ways to explain here, but a couple key ones are:

It’s doable to set Fortress up on your own servers, but you’d need to roll up your sleeves and go through the developer/platform documentation of Fortress, which is quite extensive. GridPane will give you an “Easy Button” for this.

How does this compare to a paid plan at CloudFlare?

Completely orthogonal, Fortress has no features that a CloudFlare paid plan (or any other CDN) would give you, and the opposite is also true.

You’d want both.

As an example:

Fortress can’t protect you against denial-of-service attacks. That would be ineffective because when a request hits Fortress, most of the HTTP request/response lifecycle has already been completed, and you’d be saving very few resources. Cloudflare could block it from reaching your server.

On the flipside, Cloudflare can’t touch your WordPress password hashing.

Application-layer security (Fortress) vs. network-layer security (CF).

Can 2FA only be used for admin vs user accounts?

Yes, that’s totally possible. 2FA works like this in Fortress:

