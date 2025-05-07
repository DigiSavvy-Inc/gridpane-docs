# Using DNS Made Easy (DNSME) with GridPane | GridPane

# Using DNS Made Easy (DNSME) with GridPane

 

6 min read 

### Table of Contents

 

 

### Vanity Name Servers

If you're using vanity name servers with DNS Made Easy you will need to assign the vanity name server to the domain you're using. Our API integration does not automatically add this manually in your account. Please see this section for all the details.

## Introduction

Most PaaS Cloud VPS providers include DNS management as part of their platform, the same is usually true for your domain registrar.

While these solutions may be adequate in most situations, there is a lot to be said for using a specialist DNS provider. As with every aspect of your technology stack it is generally considered best practice to separate concerns and use different specialist services for each component. This will provide greater resilience, is more secure, and when using service APIs is often more convenient.

GridPane has built in integration with DNS Made Easy (DNSME), one of the leading managed DNS providers.

To use the GridPane DNSME integration to manage your GridPane WordPress site’s DNS records you will need to have a current subscription to one of the DNSME plans that includes RestAPI access, you can find more details here.

 

## Step 1. Register your domain with DNS Made Easy

DNS Made Easy has an easy to follow video tutorial on their website which details the step by step process to register add your domain to their managed DNS service.

Make a copy of the Name Servers which you are provided for your domain, you will need to register them with your domain registrar in the next step.

 

## Step 2. Configure DNSME Name Servers at your Domain Registrar

Now you need to make sure your domain registrar is using the DNSME Name Servers for your domain. Each domain registrar has a different terminology and settings process to do this, but in most cases it is very similar.

There are too many domain registrars to provide details on how to achieve this for every single company, however please find below links to the relevant support articles for many of the most popular domain registrars.

Links to articles for some of the most popular domain registrars:

 

## Step 3. Copy your DNSME API Credentials

You can find your DNSME API Key pair in your Account Information in your DNS Made Easy console. You can navigate there through Config dropdown menu item in the top navigation bar.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1038'%20height='149'%20viewBox='0%200%201038%20149'%3E%3C/svg%3E)You will find your API Key and Secret Key at the bottom of your Account Information page.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1053'%20height='621'%20viewBox='0%200%201053%20621'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Using-DNS-Made-Easy-DNSME-with-GridPane/5d77be3787563.png)If you have not generated an API Key and Secret Key pair yet, then this area will be blank.

In that case you will need to Generate New API Credentials, to do that simply check the provided checkbox and click save. The page will refresh and you will be provided with the credentials you need.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='765'%20height='105'%20viewBox='0%200%20765%20105'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Using-DNS-Made-Easy-DNSME-with-GridPane/5d77be38838eb.png)Copy your API Credentials, including both the API Key and the Secret Key, to your clipboard.

 

## Step 4. Enter your DNSME API credentials into GridPane

Now go to your User Settings in GridPane by clicking on the Your Settings menu item in the dropdown menu accessible by clicking on your username and icon.

Click on Integrations in the left horizontal settings navigation menu, and then DNS Providers and DNS Made Easy.

Give your key a name and then enter the DNSME API Key in the API Token field, and the Secret Key in the Secret Token field and click Create.

Your DNSME API Credentials will be saved and displayed in the DNS Made Easy Account Tokens panel.

If you wish to update your credentials at a later date you can do this by clicking on the down arrow followed by blue pencil icon button.

If you wish to delete your credentials entirely, you may do this by clicking on the X button.

You can now use the DNSME API to automatically update DNS records when you provision a GridPane WordPress site.

 

## Step 5. Provision a GridPane site using DNSME to Update DNS

Next provision your GridPane WordPress site. We have an easy to follow guide that takes you step by step through the process here.

Head to your sites page, enter your new site details and then select the Dnsme option you want to use from the dropdown:

Then select the key you wish to use:

Your site will provision as normal. When it is complete it will appear in the Active Sites panel.

If you haven’t already set DNS records for this website, the API integration will create your DNS records for you. If they already exist, you can edit them to point to your new server IP by clicking on the websites name to open up the configuration modal, navigating through to the domains tab, and clicking on the server icon:

This will bring up the DNS record selection. You can manage your A records, CNAME records, TXT records and NS. Click on the type of record you’d like to edit, and here you can either add a new record or edit an existing record:

Edit your record and hit save:

 

## Custom /Vanity Name Servers and DNSME

 

If you’re using vanity name servers you will need to assign your name servers to your domains. This can be done individually or you can apply it to all of your domains as the default setting.

To set this for an individual domain, navigate to it’s Settings tab, and select your name server template from the “Applied Template” dropdown.

To set them as the default, navigate to ‘Advanced Vanity Name Servers‘ and select the desired name server. Once this is done you will see a checkbox for ‘default‘. Check this and it will set the configured name servers as the default for your domains.

For complete, step by step instructions on how to correctly set these up, please see this article over at DNSME:

How to set up Vanity DNS

It’s important to make sure this is set correctly to prevent any DNS-related errors such as SSL certificate provisioning/renewal failures or downtime.

### About Our Integration

What our integration does is ensure that if custom nameservers are being used, the SSL DNS checks will still go through correctly.

The DNS API integrations check the nameservers of the managed domains and by default it expects them to return cloudflare.com or dnsmadeeasy.com. If there are vanity nameservers that haven’t been added inside of GridPane these checks will fail. If they are added, the system knows to accept these nameservers when running checks.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

