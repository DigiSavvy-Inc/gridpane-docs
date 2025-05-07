# Why do I see a different site than I’m supposed to, an SSL warning, signon.php, or too many redirects? | GridPane

# Why do I see a different site than I’m supposed to, an SSL warning, signon.php, or too many redirects?

 

5 min read 

If you’re visiting a site and seeing a different site than expected, or an SSL warning, or a weird “Your sessions has ended”, there are a couple of scenarios for it, but it always ties back to not having a valid SSL.

Below will walk you through the common scenarios and provide links to the appropriate knowledge base articles to get you up and running.

 

## 1. You already have an SSL Certificate

If you already have a valid SSL certificate, but you’re seeing a redirect error, this is almost always a Cloudflare issue (and it’s an issue that is directly caused by Cloudflare, not GridPane). Below will walk you the most issue we see when people first move to GridPane.

The exception to this rule is that your website has an internal redirect that will need to be located and fixed.

 

#### Symptom: You see “too many redirects”

Cause: Most of the time we see this with Cloudflare users who have SSL mode set to flexible.

Solution: Set the mode to full (strict).

How to use Cloudflare SSL with GridPane sites?

 

 

### Note

Cloudflare states the following "Encrypts end-to-end, but requires a trusted CA or Cloudflare Origin CA certificate on the server” and by turning SSL on in GridPane, you get a Let's Encrypt certificate which is a trusted CA.

#### Symptom: You’re being redirected to staging or a previous URL

If routing for your domain is set to “None” (and not “root” or “www”), then you may have the incorrect address set within the database inside the wp_options table.

Previously, we used to strictly control these values. However, now that third-party services such as Cloudflare APO can work correctly, we now only control these values when you specifically set either the root or www routing type.

You can learn more about routing here:Manage Site Domains and Site Routing (non www vs www)

To check, head to the Sites page inside your account, and open up PHPMyAdmin for your website by clicking the database icon:

Click through to the wp_options table:

Here make sure your siteurl and home are set correctly. If you need to edit them, simply click on the incorrect link to edit, and then press Enter when it is correct.

 

## 2. Missing SSL Certificates

The following issues are all related to not having a valid SSL certificate on your website. To remedy them, you can follow these knowledge base articles to provision an SSL certificate.

### Webroot Method

If you are not using one of our DNS API integrations, you will need to ensure that your DNS records are first in place and follow this article:

Provisioning an SSL for a domain using Webroot Domain Verification

### DNS API Method

If using our DNS API integration, following this article:

Provisioning an SSL for a domain using DNS API Domain verification

### DNS API by Proxy Challenge Method

If the websites DNS isn’t managed inside your DNSME or Cloudflare account but you need to provision an SSL before setting the website live, please see this article:

Provisioning an SSL for a domain using DNS API Domain verification by Proxy Challenge

 

#### Symptom: You see a “Your session is finished” or a signon.php link.

Cause: This is normal Nginx behavior. It chooses another site that has a valid SSL certificate and sends you to it. This happens when you don’t have a valid certificate on the site you’re attempting to access.

Solution: Add SSL using standard webroot, or using a DNS API integration with Cloudflare or DNSME if your website’s DNS is not pointing to the server.

Alternatively, access your site via http instead of httpS. Note that Chrome often tries to force you to SSL if it has seen this site on SSL before.

 

#### Symptom: If you visit a site by httpS://site.url before you’ve toggled SSL on, you may see a warning, and if you click through that warning, you may see a different site.

Cause: This is normal nginx behavior. It chooses another site that has a valid SSL certificate and sends you to it. This happens when you don’t have a valid certificate on the site you’re attempting to access.

Solution: Add SSL using standard webroot, or using a DNS API integration with Cloudflare or DNSME if your website’s DNS is not pointing to the server.

Alternatively, access your site via http instead of httpS. Note that Chrome often tries to force you to SSL if it has seen this site on SSL before.

 

#### Symptom: Visited a site, but no warning popped up, and seeing a different site.

Cause: If you’re using Cloudflare and have SSL mode set to Full, it will have this behavior. It basically silently ignores the error.

Solution: Add SSL using standard webroot, or using a DNS API integration with Cloudflare or DNSME if your website’s DNS is not pointing to the server.

Change the Cloudflare SSL mode to Full (Strict).

 

#### Symptom: Visited site as http://site.url, but it sent me to httpS://site.url.

Cause: Sometimes Chrome remembers that the site used to be at httpS, and so it will force you. It could also be a force SSL plugin like Really Simple SSL.

Solution: Try using Chrome Incognito mode, or check for the existence of a plugin forcing SSL. Alternatively, add SSL using standard webroot, or using a DNS API integration with Cloudflare or DNSME if your website’s DNS is not pointing to the server.

 

## Further Reading

Working with SSL certificates is an important part of hosting. We highly recommend that you also check out these articles for a detailed look at why SSL certificates fail to provision and how to fix other SSL related issues:

Diagnosing and Fixing SSL Certificate Issues

How to use Cloudflare SSL with GridPane sites?

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

