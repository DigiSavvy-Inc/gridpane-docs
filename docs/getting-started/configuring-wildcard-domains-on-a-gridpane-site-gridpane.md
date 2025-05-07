# Configuring Wildcard Domains on a GridPane Site | GridPane

# Configuring Wildcard Domains on a GridPane Site

 

4 min read 

GridPane includes functionality in the Control Panel to manage and configure the domains for your WordPress sites. Every site has a primary domain, but you can also add unlimited alias domains and 301 redirect domains to any GridPane site.

If you want your site to server many subdomains of its primary domain (or indeed any of it’s domains), then it might not make sense to add these subdomains as separately, but instead configure the primary domain (or domain in question) as a wildcard domain, so that it’s server configuration will also automatically serve all subdomains as aliased domains (or even redirect domains).

For example, let’s say we have a site with the primary domain of an-example.site, and we wish to also serve whatever.an-example.site and else.an-example.site from the same WordPress site, a common use case for something like a subdomain WordPress site. We could add each subdomain to the domains manager, or we could just flip a GridPane toggle… we love toggles!

This article will run through this exact process of configuring a site with the primary domain of an-example.site to be a wildcard domain that can serve any subdomain.

In this article we will be reconfiguring a site’s primary domain to serve as a wildcard primary domain, however the GridPane domains manager will allow you to wildcard any domain attached to a site, including wildcard alias domains and wildcard 301 redirect domains.

NoteWhen making changes to site domain configurations you must disable any caching and clear any existing cache.

## Step 1.  Go to the Sites Section of the GridPane Control Panel

Click on the sites link in the GridPane main menu to go to the Sites management page.

## Step 2. Open the Site Customization Panel for your Active site

In the Active Sites panel, click on the domain in the URL column to open the Site Customization pop up box for the site you wish to update.

## Step 3. Reconfigure domain to wildcard in GridPane

Open the domains manager tab of the site customizer.  Locate the wildcard toggle for the domain you wish to configure.

Toggle wildcard on

It will take a little time for your server to adjust Nginx to a wildcard domain configuration, when the process is complete you will receive a success notification in the top right of your dashboard.

## Step 4. Add a wildcard dns record for your domain(Automated IF using GridPane DNS API integration)

GridPane will have reconfigured your server to serve request for all wildcards of this domain. However, for traffic to be routed successfully from the internet to your server you will need to make sure you have added a wildcard record for your domain at your DNS provider or domain registrar.

You should add the following A record to your DNS records

```
host/name: *
value: {server.ip}
```

For example, for this tutorial and my  an-example.site records, I have added this at DNSME

```
name: *
value: 165.227.60.188
```

If you are using either Cloudflare Full or DNSME Full DNS API integration with GridPane, then the platform will automatically add the wildcard record to your domain’s DNS records.

You can click on the DNS icon to open the DNS record management modal to confirm.

With DNS configured correctly, you can now visit your site using any subdomain of the primary domain. In our case if I go to whatever.an-example.site I am served the site correctly.

## What about SSLs?

Don’t worry, GridPane has you covered. The platform has automations in place that can provision wildcard SSLs to cover your wildcard domains.

To provision a wildcard domain with GridPane you will need to be using one of the API integrations for provisioning an SSL. We have complete documentation on those here:

Assuming your account is set up with the correct DNS API configurations, then it is as simple as enabling the SSL toggle

And waiting patiently for the SSL to enable. Wildcard SSL via DNS API integrations can take some time, please refer to the full documentation above before attempting to enable a wildcard SSL.

Once your site has a wildcard SSL securing your wildcard domain, you can visit the site via any of the subdomains of the wildcard domain by https.

In our example, whatever.an-example.siteOr, else.an-example.site

or even, another.an-example.site

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

