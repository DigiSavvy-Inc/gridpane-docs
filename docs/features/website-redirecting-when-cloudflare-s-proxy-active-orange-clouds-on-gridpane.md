# Website Redirecting When Cloudflare’s Proxy Active (Orange Clouds ON) | GridPane

# Website Redirecting When Cloudflare’s Proxy Active (Orange Clouds ON)

 

3 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

### Table of Contents

 

## Are You Experiencing an Unexpected Website Redirect With Cloudflare?

An unusual redirect issue we encountered occurred only when the Cloudflare proxy was active (as soon as the orange clouds were turned on). Upon deactivating the proxy, the redirect disappeared, and the website loaded correctly again.

The debug clearly demonstrated that the issue stemmed from Cloudflare, but it was still quite a mystery as to why this was happening.

This article details the source of the problem and how to solve it if it occurs on any of your websites.

 

## Cloudflare SaaS Partners

The issue can happen if your domain was previously registered with a Cloudflare SaaS partner. Technically, it’s not actually a redirect, it’s Cloudflare pointing the domain to the A record of the previous SaaS partner.

The SaaS partner service offering allows partner providers to use Cloudflare’s features on their customers’ domains, which means that Cloudflare’s SSL certificates, hostnames, security settings, and performance settings are all set up to be managed in a completely different account from your own.

### Hostname Priority

The partner should have removed your domain after they ceased providing their service, but in the case we’ve seen, the domain had not been officially “offboarded.”

Until your website is offboarded from their account, you won’t be able to manage any of the regular Cloudflare settings until you retake control.

This is due to “Hostname Priority.” If multiple Cloudflare setups exist for the same hostname, only one can take effect. Cloudflare for SaaS partners works differently, so it is prioritized over your regular DNS setup.

### What To Do If A Previous Provider Has Not Offboarded Your Domain

You potentially have three options to retake control of your hostname – if you’ve only recently registered the domain, then you’ll only have options 2 and 3:

 

## Liberate the Hostname

Liberate the Hostname is a third-party service that allows you to take control of your hostname from the current SaaS partner provider. They will then offload it to allow you to take back control.

This is likely the quickest way to resolve this issue for your website. Also, if your website is on Cloudflare’s Free tier, you can’t contact their support team to help resolve the issue, so it’s likely your only option.

The service can be found here and provides clear instructions for the whole process.

https://liberate-the-hostname.pages.dev/

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

