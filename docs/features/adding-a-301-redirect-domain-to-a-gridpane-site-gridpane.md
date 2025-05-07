# Adding a 301 Redirect Domain to a GridPane Site | GridPane

# Adding a 301 Redirect Domain to a GridPane Site

 

5 min readGridPane includes functionality in the Control Panel to manage and configure the domains for your WordPress sites.

The primary domain of the GridPane site is what we think of when we think of the site URL, but it is possible to add unlimited Alias domains and Redirect domains to any site using the domains manager from the site customizer.

This article will run through the process of adding an additional 301 redirect domain to a site with the primary domain of an-example.site.

The redirect domain that will be added to the site is an-example.website

301 Redirect domains are most useful for creating permanent redirects from an old domain to a new domain, this may be necessary when redeveloping a site and the owner decides to change their URL to a newer better URL. The 301 redirect ensures that any traffic from the old domain is permanently redirected to the new site domain and retains as much SEO juice as possible.

Note
When making changes to site domain configurations you must disable any caching and clear any existing cache.

## Step 1.  Go to the Sites Section of the GridPane Control Panel

Click on the sites link in the GridPane main menu to go to the Sites management page.

## Step 2. Open the Site Customization Panel for your Active site

In the Active Sites panel, click on the domain in the URL column to open the Site Customization pop up box for the site you wish to update.

## Step 3. Add the 301 Redirect domain to the Site

Open the domains manager tab of the site customizer, and click the Add Domain button

In the Create Domain modal, first enter the domain url that you wish to add. Do not include the http/s scheme, not the www host subdomain.

Next, in the Domain Type dropdown selector, choose Redirect

From the Provider dropdown, select the DNS management provider you wish to use, if any, to manage this domains DNS records and/or it’s SSL provisioning.

We currently have full DNS record integrations or and Challenge proxy (SSL only) with Cloudflare and DNSMadeeasy.

If you do not wish to use any, please select none.

Once you are satisfied with your configuration choices click the Create button, or Cancel to begin again.

Once you click create button the platform will add the domain to your site and reconfigure nginx, during this process you will see a new row appear in your domains list with the processing pending notification.

When the domain has been successfully added, you will receive a success notification in the top right of your dashboard and your domain’s row will populate with the UI elements that allow you to manage it SSL, reconfigure its nginx virtual server to serve as a wildcard domain, change it’s API integration and manage it’s DNS records, as well as to delete the domain from the site/server.

Each of these features will be explained in their own Knowledge base articles.

## What about SSLs?

In the case of our example, if you were to visit this domain an-example.website now you would be greeted with a security error.

This is because the primary site domain an-example.site has an SSL enabled, but the redirect on the server domain does not yet have an SSL. And in the case of redirects the SSL for the origin 301 domain must also contain the domains for the destination domain.

That is easily remedied by enabling an SSL, however if you had AutoSSL enabled when you added the domain then be patient, as soon as the domain has been added the system will begin the process of adding an SSL to the newly added domain.

Otherwise, just enable the SSL by following one of our guides (depending on the type of DNS management integration), it’s just a toggle away (and maybe a few clicks).

We highly recommend that you check out our guides on enabling SSL for your domains, and please reach out to support if you have any questions.

This is the only instance on a GridPane server where an SSL contains more than a single root domain.

In our example, we are redirecting an-example.website to an-example.site, so the cert for this domain will contain:

an-example.website, www.an-example.website, an-example.site, www.an-example.site

Unless you are using the wildcard implementation, in which case the following domains will be on the cert:

an-example.website, *.an-example.website, an-example.site, www.an-example.site

With both the origin and destination domains on the SSL then the redirection chain is fully encrypted and there will be no security warning.

The redirection from one domain to the other is instant and happens in the blink of an eye, but this is the most costly and problematic SSL to provision. Please make sure that all domains and their hosts resolve correctly, or are covered by a DNS API integration before proceeding.

One the SSL is enabled, you will redirect straight through

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

