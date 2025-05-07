# Nginx Helper and Custom Post Types | GridPane

# Nginx Helper and Custom Post Types

 

1 min readIf you have a website with Custom Post Types (CPTs) and you’re using our server caching, you may find that if you have an archive style page where you display these CTPs, that these are not purged from the cache automatically.

CPT pages themselves will be automatically purged by Nginx Helper, but by default, it can’t auto purge archive style pages that reference them.

To purge any of your archive pages automatically when you make a change on a CPT, you will need to manually add these to the custom purge URL option inside the Nginx Helper settings.

## Auto-Purging Custom Post Types with Nginx Helper

In your website navigate to your Nginx helper settings page:

Dashboard > Settings > Nginx Helper

Scroll down just a little until you the see the Purging Conditions as shown in the image below:

Here you can add the URLs (without the domain name) for your CPTs so that Nginx Helper knows to automatically purge them whenever you update these pages.

For example, if the page you wanted to automatically purge was domain.com/latest-news/, you would add “/latest-news/” in the outlined box. Add 1 URL per line.

Below is an example of how this looks:

Once you’ve added your URLs, just click the Save All Changes button to finish up and you’re all set.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

