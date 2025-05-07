# Adding SSL certificates to GridPane Sites - An Overview | GridPane

# Adding SSL certificates to GridPane Sites – An Overview

 

4 min read 

It is very easy to add SSL Certificates from the free Let’s Encrypt Certificate Provider to the domains associated with your GridPane site. This will allow your site and it’s domains to be served by the encrypted HTTPS protocol, and your visitors will also benefit from the speed increased enabled by HTTP2 which only works via HTTPS.

 

 

### Auto SSL Information

GridPane has an Auto-SSL feature available from the settings tab of your site customizer. This is only necessary for websites such as WaaS networks where you would like to auto attempt for SSL certificates as you add additional alias and 301 redirect domains inside the domains tab. 
It is NOT recommended for regular websites. To find out about this feature, please check the link to AutoSSL documentation at the bottom of this page.

Full management of SSL certs for domains attached to GridPane managed sites is handled by the Domain manager tab in the site customizer:

This approach means your site’s domains all have separate SSL certificates.

There are several benefits to this approach, most notably the fact that there is no “site” SSL, so there are no limits to the number of domains on an SSL for your site. Your site can have as many domains as you like, and each domain has its own discrete SSL. This also means that a problem with DNS for one domain will never affect the SSL certificate for another domain on your site.

GridPane also utilises 3 different methods to verify domains for the provisioning of SSL certificates:

For the DNS API integration methods of domain verification, we currently support two of the most popular DNS management providers (we will be adding more shortly):

These DNS integrations also allow us to automate the provisioning of Wildcard SSLs for any and all of your domains, including primary domains, alias domains, and redirect domains.

And every SSL for every domain can be managed independently, completely granular control of your site’s SSL certificates.

Sweet!

Given these options and control we are providing, we figured it was best to break this Knowledge Base article out into separate articles, each clearly explaining how to provision an SSL using that specific method.

 

 

## SSL Support

SSL Certificates Failures
For assistance with SSL certificate related issues, please ensure you attach the info from your SSL provisioning logs when contacting support/posting in the community forum so that we can quickly assess what's going on and assist you as fast and efficiently as possible.
How to Create a Support Ticket
DNS Checks / Console Output / Screenshots
Please provide as much relevant information as possible - check if your DNS is live,  check console output on your site (right click > inspect element > console), and attach any relevant screenshots of errors.

Too Many Redirects Error
If you're using Cloudflare with GridPane, please ensure you have the correct SSL settings to prevent redirect errors:How to use Cloudflare SSL with GridPane
SSL Locks and Rate Limiting
If multiple SSL attempts fail, GridPane will place an SSL lock to prevent you from getting rate limited by Let's Encrypt. It's important to assess why your SSL's are failing and correct the issue. Learn more about rate-limiting and how to remove locks here:GridPane SSL Locks and Let’s Encrypt Rate Limiting
SSL Troubleshooting Guide
This article will help new users prevent common SSL issues, and learn how to diagnose the more complex ones.
Diagnosing and Fixing SSL Certificate Issues
SSL Renewal Failures
If you're receiving notifications that one of your SSL certificates has failed to renew, Let's Encrypt will return the exact reason for failure inside the Certbot or Acme monitoring logs.

Monit SSL Renewal Failure Notification in the Dashboard or Slack
Mixed Content / No Padlock
If you've provisioned an SSL but don't see a padlock, please check for images and/or other content being served over HTTP instead of HTTPS. It's likely you need to update your database to serve links over HTTPS:
Why Am I Not Seeing a Padlock on my Site?

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

