# Why Do SEO Tools / LinkedIn Say My Website is Insecure? | GridPane

# Why Do SEO Tools / LinkedIn Say My Website is Insecure?

 

1 min read 

## Latest TLS Versions NOT Supported

At the time of writing, if you’re forcing TLS 1.3 on your websites, LinkedIn, as well as some SEO tools, will report that your website is insecure, even though you have an active SSL and are using the latest secure protocols.

This is due to them not supporting the latest TLS version (despite the fact that TLS 1.3 was released in August 2018), and is a quick and easy fix.

## The Solution

If you’re using Cloudflare and forcing TLS 1.3, then you might run into this issue.

Inside your Cloudflare account, click through to your domain, and from the menu, select SSL/TLS > Edge Certificates.

Here, you’ll see an option titled “Minimum TLS Version“. From the dropdown, change the option from TLS 1.3 to TLS 1.2.

The tool that was reporting that your website is insecure should now see it as secure.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

