# New Website Checklists | GridPane

# New Website Checklists

 

7 min read
## Introduction

In this article, we’ll take a look at the things you’ll want to have in place when you’re launching a new website on GridPane.

In a nutshell, you’re going to want an SSL certificate, transactional email (for contact form submissions, etc), your security setup, caching, and your DNS records in place.

The order in which you do these will depend on whether you’re using a DNS API integration with either Cloudflare or DNS Made Easy (DNSME).

If you’d like to skip ahead, these are the main sections of this article:

## To-Do’s for Every Website

### Transactional Email

Before you set your website live, you need to ensure that it’s properly configured to send email. This ensures that contact forms will function correctly, and you’ll receive any necessary notifications from WordPress and any plugins that send alerts/updates.

We integrate with Sendgrid, but you can setup SMTP using a plugin such as WP Mail SMTP and hook your website up to a variety of other providers such as Sendinblue, Amazon SES, Mailgun and more.

### Security

It’s a good idea to create your own security plan that you can follow, and also help your clients implement.

You can learn what GridPane secures by default here along with further recommendations: Default GridPane Security and Additional Options

We recommend you:

### Implement Caching

We highly recommend our server-side caching options. We offer Redis Nginx Page Caching or FastCGI page caching, and also Redis Object caching.

You can choose one of the two page caching options and combine it with Redis Object caching for exceptional performance. Please check out this article for an introduction on exactly what our server caching options are and what they do:An Introduction to GridPane Server Caching Options

If you’re not using our server-side caching, then make sure you toggle off caching inside your website’s configuration modal. Our caching will not work well with other regular caching plugins and in fact, may break your website’s appearance on the front end. You can also turn off Redis object caching by deactivating the plugin inside your website.

### Provision an SSL Certificate

This almost goes without saying, but since it’s a checklist, we’ll say it: You should provision an SSL certificate. You can do this a couple of ways – either by using the webroot domain verification method (which requires setting DNS records and letting them propagate worldwide before you can provision):Provisioning an SSL for a domain using Webroot Domain Verification

Or you can use the API method. This allows you to provision an SSL before changing your DNS records. Learn more here:Provisioning an SSL for a domain using DNS API Domain verification

Don’t toggle on AutoSSL unless you need it. Learn more here:Using GridPane AutoSSL

### Set your DNS Records

DNS records are pretty straightforward once you know what you’re doing. If you’re new to managing your own DNS, please check out our article on it here:Setting DNS Records

You can also manage your DNS records directly inside your GridPane control panel if you’re using either our DNS Made Easy or Cloudflare API integration.

We recommend setting your DNS live after you’ve checked all the above boxes and ideally provisioned your SSL. Note that with some DNS providers, it can take a few hours, sometimes even longer, for DNS records to propagate worldwide. You can keep an eye on yours with this website:

DNS Checker – DNS Check Propagation Tool

If you’re using the webroot method for provisioning an SSL, toggle SSL on once the IP address is live everywhere worldwide.

## New Brochure Website Checklist

## Ecommerce Store Considerations

### Server Considerations

Ideally, your ecommerce store will live on its own server, with no other websites. If it’s small in size and traffic, you may be fine with a 1CPU 2GB RAM VPS.

### MySQL RAM Allocation

Ecommerce can be heavy on resources. You’ll want to take advantage of Redis Object caching to reduce the workload off MySQL, and you may want to monitor MySQL usage and increase its RAM allocation if required. You can learn how to do this here:Adjusting MySQL Monit Memory

### Cache Exclusions

If you’re using our server caching and your store is not in English, OR if you have custom URLs, you will also need to exclude the shopping cart and checkout pages from the cache. By default, we exclude the following:

These pages won’t function correctly if the server or a caching plugin is serving up a pre-stored copy.

You can learn how to exclude specific pages from your website’s cache here:Exclude a page from server caching

## New Ecommerce Store Checklist

## WaaS Network / WP Ultimo Considerations

### MySQL RAM Allocation

Like Woocommerce stores, Ultimo stores are also heavy on MySQL usage. Issues usually arise when the server is simply too small for the website. For best performance, your entire database should be stored in RAM, and your server needs to be large enough to accommodate this.

You’ll want to take advantage of Redis Object caching to reduce the workload off MySQL, and you will want to monitor MySQL usage and increase it’s RAM allocation as required. You can learn how to do this here:Adjusting MySQL Monit Memory

### Custom Sign-Up URL Cache Exclusion

By default, any URL that ends with “.php” is excluded from the cache. WP Ultimo gives you the option to set a custom sign-up URL. Learn how to exclude this here:Exclude a Custom WP-Ultimo Sign-Up URL from the Cache

### Wildcard SSL and AutoSSL

GridPane has an awesome integration with WP Ultimo. If you add a subsite to your network with an alias domain, it will automatically be added to your website’s domain tab inside of GridPane, and automatically try to provision an SSL certificate for that domain. Learn more here:Using GridPane AutoSSL

Provisioning a Wildcard SSL for a domain using DNS API Domain verification

### Backup Schedule

By default, GridPane local backups take place every hour on the hour. Depending on the size of your WaaS network, this may put a strain on your server’s resources resulting in table locking and poor performance. You may wish to adjust your schedule to just once or twice per day during the quietest hours.

You can learn how to adjust your backup schedule here:GridPane Local Remote Backups

And you may wish to check out this article for further information on performance:Why is my WaaS network slow – Table locking and MySQL RAM allocation

### Transactional Email

The default SendGrid integration doesn’t allow for customizing the “From” email for subsites. You’ll want to look for a solution that works with your chosen SMTP provider and allows the from address to be customized.

## WaaS Network / WP Ultimo Checklist

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

