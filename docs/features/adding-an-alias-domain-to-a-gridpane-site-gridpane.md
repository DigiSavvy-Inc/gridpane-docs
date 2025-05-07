# Adding an Alias Domain to a GridPane Site | GridPane

# Adding an Alias Domain to a GridPane Site

 

4 min read 

GridPane includes functionality in the Control Panel to manage and configure the domains for your WordPress sites.

The primary domain of the GridPane site is what we think of when we think of the site URL, but it is possible to add unlimited Alias domains and Redirect domains to any site using the domains manager from the site customizer.

This article will run through the process of adding an additional alias domain to a site with the primary domain of an-example.site.

The alias domain that will be added to the site is an-example.website

Alias domains are most useful for things like mapping subdomains to in a multisite network.

Note: When making changes to site domain configurations you must disable any caching and clear any existing cache.

 

 

### Alias vs Redirect

An alias domain is an additional domain attached to a website, meaning that both the primary domain and alias domain will take you to the same WordPress installation, and display the website under that domain name in the address bar. Alias's can be also be mapped to a subdomain or subdirectory, as is common on WordPress multisites.
Example Use Case: If you're running a WaaS network using WP Ultimo, you can map alias domains so that your clients subsites show as clientdomain.com instead of waasnetwork.com/client-name.

A redirect domain, will add a 301 redirect to your domain name, which means that when someone types this address into their browser, it will redirect them to your primary domain. It will not display the redirect domain in the address bar.
Example Use Case: You've moved your website to a new domain name but you don't want to lose either the website traffic or SEO benefits of your old domain.

## Step 1. Go to the Sites Section of the GridPane Control Panel

Click on the sites link in the GridPane main menu to go to the Sites management page.

## Step 2. Open the Site Customization Panel for your Active site

In the Active Sites panel, click on the domain in the URL column to open the Site Customization pop up box for the site you wish to update.

## Step 3. Add the Alias domain to the Site

Open the domains manager tab of the site customizer, and click the Add Domain button

In the Create Domain modal, first enter the domain URL that you wish to add. Do not include the http/s scheme, nor the www host subdomain.

Next, in the Domain Type dropdown selector, choose Alias

From the Provider dropdown, select the DNS management provider you wish to use, if any, to manage this domains DNS records and/or it’s SSL provisioning.

We currently have full DNS record integrations or and Challenge proxy (SSL only) with Cloudflare and DNSMadeeasy.

If you do not wish to use any, please select none.

Once you are satisfied with your configuration choices click the Create button, or Cancel to begin again.

Once you click create button the platform will add the domain to your site and reconfigure nginx, during this process you will see a new row appear in your domains list with the processing pending notification.

When the domain has been successfully added, you will receive a success notification in the top right of your dashboard and the Alias domain row will populate with the UI elements that allow you to manage it SSL, reconfigure its nginx virtual server to serve as a wildcard domain, change it’s API integration and manage it’s DNS records, as well as to delete the domain from the site/server.

Each of these features will be explained in their own Knowledge base articles.

## What about SSLs?

In the case of our example, if you were to visit this domain an-example.website now you would be greeted with a security Not Secure as the site and primary domain have an SSL enabled, but the Alias domain does not yet have an SSL.

That is easily remedied by enabling an SSL, however if you had AutoSSL enabled when you added the domain then be patient, as soon as the domain has been added the system will begin the process of adding an SSL to the newly added domain.

Otherwise, just enable the SSL by following one of our guides (depending on the type of DNS management integration), it’s just a toggle away (and maybe a few clicks).

We highly recommend that you check out our guides on enabling SSL for your domains, and please reach out to support if you have any questions.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

