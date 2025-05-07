# WordPress Security Resources | GridPane

# WordPress Security Resources

 

9 min read 

 

### Information

This article is a work in progress, and will be continually updated with more resources in the near future and beyond.

## Introduction

One of the most misunderstood and neglected aspects of the WordPress space is security. It is a confusing and complex topic, and there is a never ending stream of largely biased “opinions” or repurposed content to make things all the more confusing.

This reference page aims to cut through all of the noise and provide you with the resources you need to start making informed decisions about WordPress security for both your business and those your business serves.

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='683'%20viewBox='0%200%201024%20683'%3E%3C/svg%3E)

### Table of Contents

 

## 1. Before We Begin: A Trap to Avoid

The research into popular security plugins conducted by Calvin Alkan of Snicco has provided a much-needed wake-up call to the WordPress community at large. Some responses to this research have been a little surprising, so here’s a trap to avoid.

### Commitment and Consistency

In his excellent and highly influential book Influence: The Psychology of Persuasion, Robert Cialdini explains:

“Once we have made a choice or taken a stand, we will encounter personal and interpersonal pressures to behave consistently with that commitment. Those pressures will cause us to respond in ways that justify our earlier decision.”

This is the principle of commitment and consistency, and it’s something that all of us experience throughout all areas of our lives.

### The Takeaway

Just because you may have used and recommended a plugin in the past and perhaps even used it for many years doesn’t mean it’s a good idea to continue doing so.

Security plugins, in particular, need to hold themselves to the highest possible standards, and very few of the most popular plugins do so. You should hold the plugins that you use in your business to the highest standards, and, painful as it may be to change course, discontinue using them if they continually prove themselves to be incapable of meeting even minimum standards of security for their users.

 

## 2. The State of WordPress Security

Two of the companies we trust most when it comes to truthful, reliable, and accurate WordPress security information are Snicco and Patchstack. Below are their latest takes on the state of WordPress security.

### Snicco

Calvin Alkan’s security research highlights the many problems facing (and caused by) WordPress security plugins:

The state of WordPress security plugins in 2022

### Patchstack

Patchstack’s whitepaper offers an overview of the most common vulnerabilities, security trends, and more:

State of WordPress Security In 2022

### WeWatchYourWebsite

Thomas Raef published his 2023 insights, offering a deep dive into server-level root cause analysis. No security plugin has access to this kind of data, and Thomas challenges the often-repeated claim that “95% of WordPress hacks are due to outdated plugins or themes.”

Here’s what 851+ billion log entries reveal about WordPress website hacks at scale and how this is being done through authentication credential compromises, NOT through plugin or theme vulnerabilities:

The Real Attack Vector Responsible for 60% of Hacked WordPress Sites in 2023

 

## 3. How WordPress Vulnerabilities Are Exploited

More articles will be added to this section in the near future.

### Patchstack: The Most Common WordPress Vulnerabilities

Patchstack has an excellent database available, detailing 1000s of vulnerabilities, and this article provides some insight into the different types of vulnerabilities that can occur and how they’re exploited:

Most Common WordPress Vulnerabilities & How to Fix Them

### WeWatchYourWebsite: Insights from 150,000 Hacked Websites

Here’s a look behind the curtain from WeWatchYourWebsite’s clean-up of 150k hacked sites.

Thomas writes:

“Almost 60K infected sites had installed a WordPress security plugin with a malware scanner.

This report is intended to answer questions and add context to our recently announced discovery of tens of thousands of compromised WordPress websites where popular security plugins were present but unable to detect malware that added itself to the security plugins’ allow lists.”

How We Identified Nearly 150K Hacked WordPress Sites in 60 Days

 

## 4. WordPress Security Recommended Reading

We’ll continue to add valuable resources to this section.

### Security In-depth: The Swiss Cheese Method

Patrick Garman of the highly-respected WordPress agency Mindsize recently published their approach to layered WordPress security:

Malware Scanners Don’t Work, Try the Swiss Cheese Method

### What Is A Web Application Firewall (WAF)?

A WAF is an important part of your WordPress security strategy. Not 100% sure what a WAF does? Check out this article from Patchstack:

What Is A Web Application Firewall (WAF)?

### Network Layer Security and Cloudflare

If you use Cloudflare for one or more of your websites, you can take advantage of their free firewall rules to provide an additional layer of security to your websites:

Cloudflare Firewall Rules for Securing WordPress Websites

### How WordPress uses Authentication Cookies & Sessions

Authentication credential compromises were responsible for 60% of WordPress hacks in 2023. This is one of the most important areas of WordPress security, and Calvin Alkan has published the definitive guide on the topic here:

How WordPress uses Authentication Cookies & Sessions: A technical Deep-Dive

### How WordPress Uses Salts and Why You Should Not Rotate Them

There’s a lot of incorrect information published around WordPress salts. This is the definitive guide and will clear up any misconceptions you may have on the topic:

How WordPress Uses Salts and Why You Should Not Rotate Them: A technical Deep-Dive

 

## 5. WordPress Security Case Study: Securing Multiple Banking Websites

As an alternative to 1000+ versions of “The Ultimate Security Guide to WordPress Security,” here’s a real-world case study of securing two websites for a multinational bank:

WP Security 2023: Securing Multiple Banking Websites Built on WordPress

 

## 6. WordPress Security Plugins: Do Your Due Diligence

Security plugins are just one part of a comprehensive security strategy for your WordPress websites, and you should be particularly cautious and do your due diligence when choosing a plugin.

### Security Plugin Vulnerabilities

Before you install a security plugin, I’d highly recommend checking their history and looking at whether

Check out the security research by Snicco and the Patchstack vulnerability database (learn more here).

### Should You Use a Security Plugin?

Here’s our take on the pros and cons of WordPress security plugins. This article was originally for the GridPane community, but the information is no less relevant to websites being hosted elsewhere.

Do I Need a Security Plugin When Using GridPane’s Security Features?

### Recommended: Fortress

GridPane has an integration with the excellent Fortress security plugin by Snicco. This is integrated at the server level and provides the following features:

Fortress is the only security plugin that we officially recommend, and it provides effective application-level security that most plugins either do incorrectly, insecurely or not at all.

### Also Great: Patchstack

Patchstack is a really interesting option for vulnerability monitoring and virtual patching (patching is a paid feature). They are laser-focused on this one aspect of security, and you can even use their free plan to update plugins on your websites directly from their dashboard instead of having to do it manually site by site.

Patchstack.com

### WP Builds Podcast Security Series

In 2023, the WP Builds Podcast put together a unique 4 part security series where all episodes were recorded before any episodes were released and then published one by one. Two prominent members of our community took part in the series – Calvin Alkan and Thomas Raef – and the entire series is now available to listen.

Calvin addresses many of the issues that have been prevalent in WordPress security plugins, making his research accessible in a way that anyone, no matter their skill level, can understand.

I’ll provide a brief intro for episodes 2-4 in the near future.

 

## 7. The Limitations of Plugin Malware Scanners

Here’s an eye-opening deep-dive that explains why everything you know about your WordPress Malware Scanner is WRONG.

This research was a collaboration between GridPane, Calvin Alkan of Snicco, and Thomas Raef of WeWatchYourWebsite, and was then independently verified by Patchstack.

Malware Madness 1/2: Why everything you know about your WordPress Malware Scanner is wrong

Part 2 will be available soon.

 

## 8. Dealing with Malware/Compromised Websites

Cleaning up malware is a job for a security professional, not a plugin, and probably not you, unless you have the appropriate experience. Far too many people put their trust in plugin-based malware scanners and one-click cleanup solutions, only to be quickly compromised again and seek advice claiming that they had previously successfully cleaned up their site’s infection.

That said, hopefully, the following will help should one or more of your sites ever get compromised.

### First Steps When Dealing With Malware

While dealing with malware is a task for an experienced security professional, this article offers some tips for your first steps when dealing with a site that has been compromised with malware.

First Steps When Dealing With a WordPress Malware Infection

### Malware Cleanup Services

While many services exist, we’ve only ever recommended one firm for cleanup and root cause analysis: WeWatchYourWebsite.com

 

## 9. Strategies for Dealing with Spam

Spam is both a nuisance and has security implications. You don’t need costly, resource-heavy plugins for an effective anti-spam strategy.

### Block Contact Form Spam

How to Reduce Eric Jones Spam (and all the other Contact Form Spam)

### Block Comment Spam

How to Stop WordPress Comment Spam Permanently (for FREE)

 

## 10. Recommend Resources for Reliable WordPress Security Information

Like so many of the links above, the following resources from Snicco, Patchstack, and Wordfence are great WordPress security resources. We’ll add more here in the near future, and for GridPane users, also see the next section below.

### Patchstack Vulnerability Database

Patchstacks database is an excellent resource to learn more about the different vulnerabilities that can affect your website and look up the history of plugins you may be considering using:

Patchstack Vulnerability Database

### Wordfence Vulnerability Database

Wordfence also has a very extensive vulnerability database as well, and they’ve also made it 100% free for commercial use:

Wordfence Intelligence: WordPress Vulnerability Database

### Snicco Vulnerability Disclosures

Calvin Alkan has researched, responsibly disclosed, and provided security fixes (completely free of charge) to almost every well-known security plugin and has made all of this work publicly available. It offers insights into how different plugin vendors:

Snicco Vulnerability Disclosures

### Patchstack Blog

Patchstack regularly publishes high-quality security-related content and is a great resource for learning more about WordPress security as a whole.

Read the Patchstack Blog

 

## 11. GridPane Specific Reading

If you’re hosting websites with GridPane then we have a ton of reading material available. You can view our security step-by-step learning path here:

WordPress Security Step by Step

And the full security section of our knowledge base here:

Knowledge Base: Security

 

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

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

 

 