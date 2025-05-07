# Resolving the “This site can’t be reached, ERR_NAME_NOT_RESOLVED” error | GridPane

# Resolving the “This site can’t be reached, ERR_NAME_NOT_RESOLVED” error

 

2 min read 

We see this come up on support regularly, especially for staging websites. It looks as follows:

This means that no DNS records exist for this domain, so when you try to access it in your browser, it has no way of knowing where to go to download the files, and so ultimately returns this error.

## Checking Your DNS

This website is an excellent resource for checking DNS records. It’s what our team use, and we highly recommend that you bookmark it for future use as it comes in handy when changing DNS records and seeing its current state across the world:

DNS Checker – DNS Check Propagation Tool

If you have no DNS records in place, it will look like this:

## To Resolve this Error

To be able to access the website, you will need to create the DNS records for it to be accessible over the internet.

Below is an example of how an A record and CNAME for your primary website and staging website will look:

In your case, “example.com” would of course be your own domain name. For your site, you will need to create the missing records, and you can then check on their status using the DNS Checker website linked above. Once they are live in your location, you will be able to access your website.

You can learn more about managing DNS here:

Setting DNS Records

### DNS API

If you’re using our Cloudflare or Let’s Encrypt integration on a website, these will automatically create DNS records for your sites where they don’t already exist. This can be a handy time-saver for staging sites that have no existing records.

You can learn more about our DNS API integrations here:

Using Cloudflare with GridPane

Using DNS Made Easy (DNSME) with GridPane

### Additional Note

This is also particularly handy for SSL certificates if you’re using the Webroot method, which requires your DNS to be fully propagated worldwide before Let’s Encrypt will grant your website an SSL.

## Further Reading

If you wish to view your websites without setting DNS records, you can check out this article:

How can I edit my local hosts file to redirect URLs

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

