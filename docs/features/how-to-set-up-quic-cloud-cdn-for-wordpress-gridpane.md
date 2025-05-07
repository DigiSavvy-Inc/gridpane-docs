# How to Set Up QUIC.cloud CDN for WordPress | GridPane

# How to Set Up QUIC.cloud CDN for WordPress

 

6 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

## Introduction

QUIC.cloud is LiteSpeed’s own CDN product built specifically for WordPress. The LiteSpeed Cache plugin directly integrates with the CDN, making it highly configurable and easy to manage. If you need a CDN for an OLS site, this is an excellent option that offers great value for money.

In this article, we’ll take a look at how to get up and running with OpenLiteSpeed and QUIC.cloud, but the same steps apply to any LiteSpeed server.

### Table of Contents

You can also see the official documentation from LiteSpeed here: https://docs.litespeedtech.com/lscache/lscwp/cdn/

 

 

### SSL Notice

You should have no issues using GridPane SSL certificates, however, always be sure to pay attention to your notifications just incase it fails to renew for any reason.

## About QUIC.cloud

QUIC.cloud bills itself as “the only CDN service that can accurately cache dynamic pages (pages that can change frequently).” It’s easy to configure and has multiple WordPress and network security configurations available, including DDoS protection.

Along with the CDN, additional features also include image optimization, CDN-level reCAPTCHA, brute force login protection, and critical CSS generation.

The CDN integrates directly with the LSCache plugin, and there’s a free tier available that may be enough for some low-traffic websites. It’s an interesting offering, and you can learn more about pricing and sign up directly on their website here: https://quic.cloud/cost/

 

## Creating a QUIC.cloud Account

Creating an account is quick and easy, and it’s also free. You’ll be allocated a set amount of free quota credits (50 per month at the time of writing), and then paid extras are optional.

If you already have an account you can login now.

### Create Your Account

Click here to open up the website, and enter your email to get started. You’ll be taken to a new page to set your password, and then a confirmation email will be sent out. Verify your account through the email, and then you’re all set.

 

## Enabling QUIC.cloud Inside of WordPress

Login to your WordPress website and navigate to Dashboard > LiteSpeed Cache > General.

 

### Linking Your Website to Your Account

To begin, first click the “Request domain key” button. This may take a minute or two to go through.

Once you have your domain key, click the “Link to QUIC.cloud” button that is now active:

Once connected you’ll see your website in your CDN dashboard, and you manage it by clicking its name:

 

### Turn QUIC.cloud CDN ON

Finally, we need to activate the CDN inside your LiteSpeed cache settings. When this is inactive, you’ll see a notification inside your QUIC.cloud account CDN settings that this first needs to be enabled before it can be configured:

Navigate to your Dashboard > LiteSpeed Cache > CDN settings page, and toggle the CDN to ON:

You’re now ready to configure your CDN.

 

## Activate the CDN Settings

Inside the CDN settings page, click through to the “QUIC.cloud CDN Setup” tab.

Here, click the “Begin QUIC.cloud CDN Setup” button:

 

## Update Your DNS Nameservers

In order to use QUIC.cloud you’ll need to point your nameservers to their platform. Once you activate the CDN, you’ll receive an email with those nameservers:

And you can also view them further down the CDN Setup page inside your website as well:

Once updated, you’ll receive another email letting you know:

And inside your website you’ll see the same confirmation (you may need to click the setup button again):

 

## SSL Certificates

As you’re not using one of our DNS integrations now that your website’s nameservers are pointed to QUIC.cloud, and your A and CNAME records are no longer pointing towards your GridPane server, there are a couple of important things to be aware of when your CDN is active.

 

### 1. QUIC.cloud Generated SSL Certificate

QUIC.cloud should automatically attempt to provision a new SSL for your website. However, this may take a little time to complete – in my case, when writing this article, it took around 6 minutes:

Once provisioned you’ll be able to see its status:

Its validity will be 90 days, and it will automatically renew.

 

### 2. Using a CDN and GridPane SSL Certificates

You should still enable an SSL certificate at GridPane for your website, and even though your A/CNAME records are pointing to different IPs all around the world, you should have no issues with provisioning a new SSL or renewing your SSL certificates.

In my testing writing this article, I confirmed all of the above. However, you should always pay attention to your GridPane notification and check your SSL logs if a renewal failure is reported.

 

## How to Check Your Page and CDN Caching

To check if QUIC.cloud CDN is serving your site you can use LiteSpeed’s LSCache Check tool here.

Enter your URL and hit the Check button. The tool will then confirm your caching status and display your site’s response headers. Look for the x-qc-pop header.

If this is present, then it was served via a QUIC.cloud PoP, and your CDN is active and configured correctly.

Note that it may not be a HIT response for the CDN on your first load. However, if you refresh the page, it should then show a HIT (assuming it’s been served from the same PoP).

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

