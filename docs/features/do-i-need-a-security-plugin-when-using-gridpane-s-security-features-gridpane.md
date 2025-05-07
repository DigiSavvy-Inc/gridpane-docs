# Do I Need a Security Plugin When Using GridPane’s Security Features? | GridPane

# Do I Need a Security Plugin When Using GridPane’s Security Features?

 

6 min read 

 

### Important

This article and its recommendations have been updated since it was originally published. We highly recommend you check out Calvin Alkan's research into security plugin vulnerabilities before deciding to install one on any of your websites:
WordPress plugin vulnerabilities

## Introduction

GridPane offers a lot of security out of the box, and then a whole suite of WordPress specific security measures that you can configure on a per website basis.

A common question we get is: ”Do I still need a security plugin when using all of these features?”.

There’s no single correct answer to this question, but in this article we’ll provide you with some guidance on making a decision for your websites.

### Table of Contents

 

## Do You NEED a Security Plugin?

If you’re using either the 7G WAF/ModSecurity WAF, Fail2Ban, and our additional security measures, then when it comes to most WordPress security plugins, our stance is probably not. The exception to this rule is Fortress (more info below).

That said, there are some additional benefits that a few security plugins can provide (some that aren’t actual security measures). In the following sections we cover some of the benefits as well as some downsides to consider.

 

## Official Recommendation: The Fortress Security Plugin

GridPane has an integration with the excellent Fortress security plugin by Snicco. This is integrated at the server level and provides the first 4 benefits outlined in the following section:

Fortress is the only security plugin that we officially recommend, and it provides effective application-level security that most plugins either do incorrectly, insecurely, or not at all.

You can learn more about Fortress and our integration in these two articles:

 

## Additional Security Benefits Plugins Can Offer

What most security plugins offer as features can only be done effectively at the server level. That said, there are some additional benefits that a plugin can offer outside of the GridPane feature set.

 

### 1. Two-Factor Authentication (2FA)

2FA, if implemented securely, offers a highly effective layer of defense to protect your websites if your username and passwords are ever compromised.

One of the biggest problems with many security plugins (both now and in the past) is that their two-factor authentication is not only NOT secure, but its activation may also have led to your website being hacked in certain circumstances. Snicco provided numerous plugin vendors with the code needed to fix such issues.

In Fortress, two-factor authentication employs the most up-to-date, best security practices, can be enforced at a granular level, and is the ONLY security plugin that rate-limits failed 2FA attempts. Without implementing rate-limiting, 2FA can be brute forced, simple as that.

 

### 2. Upgraded Password Security

WordPress uses an outdated md5-based hashing scheme for password security that is no longer considered secure. A plugin like Fortress can remedy this issue by  replacing the default password-hashing functions with up-to-date and secure cryptography.

 

### 3. Rate Limiting

Rate limiting is a technique used to control the rate at which requests are made to a system or service to prevent overload and to protect against malicious attacks, such as brute-force attacks, that attempt to flood a system with too many requests.

While this is better done at the server level, a plugin can offer protection for password resets and login attempts in a user-friendly way, instead of only banning IPs.

 

### 4. Secure Session Management

Easily the most overlooked aspect of WordPress security is secure session management. The default WordPress sessions have some major disadvantages, and can be made much more secure.

Learn more here.

 

### 5. Vulnerability Reporting and Patching

Vulnerability patching is where a service monitors your sites and identifies vulnerabilities in WordPress core, themes, and plugins, and automatically patches them (which sometimes just means updating those plugins).

The overwhelming majority of malware infections come via plugin vulnerabilities. Virtual patching and setting vulnerable plugins to automatically update can be excellent additional security measure for your websites.

Many free plugins include a monitoring and alert service, which is still useful even without the actual patching.

Patchstack is a really interesting option for vulnerability monitoring and patching (patching is a paid feature). They are laser-focused on this one aspect of security, and you can even use their free plan to update plugins on your websites directly from their dashboard instead of having to do it manually site by site.

 

### 6. Email Alerts

Finally, email alerts can be incredibly useful for passively monitoring your websites. If a security plugin detects you’re under attack, detects vulnerabilities in plugins/themes/core, and detects core file changes or malware, these are serious matters that you may otherwise remain oblivious to for some time.

Keeping track of admin logins and user activity can be beneficial on some websites too, especially if you have any “problem clients”.

 

### Limited Benefit: Malware Scanning and Core File Monitoring

This one is self-explanatory. Monitoring your websites for malware and checking core file integrity can offer peace of mind, and alert you to any issues that you need to look into on any of your websites.

That said, it’s entirely possible for malware to whitelist itself when this is implemented via a plugin instead of securely at the server level. In fact, the conventional method of plugin-based malware scanning in WordPress is flawed and conceptually impossible.

For a deep-dive into this topic, click here to see why everything you know about your WordPress Malware Scanner is WRONG.

The research in the article linked above was a collaboration between GridPane, Calvin Alkan of Snicco, and Thomas Raef of WeWatchYourWebsite, and was then independently verified by Patchstack.

 

 

### What about Automated Malware Cleanup?

Automated malware clean up is a gamble at best. Maybe it will get the job done, but there's a high chance it won't. Relying on one-click tools for this kind of specialised work is generally something we advise against, and it also won't provide you with root cause analysis. Hiring a professional or restoring a backup that you know to be clean are usually better options.

## Potential Downsides to Consider

Security plugins aren’t all upside and no downside. In fact, many of the most popular security plugins have had extremely serious security vulnerabilities themselves. Some security plugins may:

They can also provide a false sense of security, and implementing security at the application layer is far less preferable to security at the DNS and server layers, before malicious traffic even has a chance to reach your websites in the first place. 

## Final Thoughts

You shouldn’t rely solely on a plugin for securing your websites.

They can have some side benefits (as noted above). Speaking for myself, I now use Patchstack for email notifications on plugin vulnerabilities, and then I mass update them via their UI.

For further discussion, please feel free to reach out to the community to see how other developers and agency owners approach securing their sites over in the forum:

GridPane Community Forum

 

## Further Reading and Resources

We highly recommend the following blog post detailing the state of WordPress security over on Snicco.io: The state of WordPress security

We also have numerous guides on WordPress security over in the Security section of our knowledge, and we also have a learning path with a case study that you can check out here:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

