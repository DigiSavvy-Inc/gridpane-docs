# How to use Cloudflare SSL with GridPane sites? | GridPane

# How to use Cloudflare SSL with GridPane sites?

 

1 min read 

The Cloudflare redirect loop error is something we see at least once every day in support. Fortunately, it is easy to fix and prevent once you know the cause.

This is a Cloudflare specific issue. They state:

The Flexible SSL encryption mode in the Cloudflare SSL/TLS app Overview tab encrypts traffic between the browser and the Cloudflare network over HTTPS. However, when the Flexible SSL option is enabled, Cloudflare sends requests to your origin web server unencrypted over HTTP. Redirect loops occur if your origin web server is configured to redirect all HTTP requests to HTTPS when using the Flexible SSL option.

You can read the full Cloudflare article here.

## How to Fix and Prevent Redirect Loops

First, enable an SSL for your website inside of your GridPane account. Only enable this option after an SSL has been fully provisioned for your website on your server.

Please use the Full (Strict) option. This ensures a secure connection between both the visitor and your Cloudflare managed domain, and also between Cloudflare and your server.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='0'%20height='0'%20viewBox='0%200%200%200'%3E%3C/svg%3E)

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

