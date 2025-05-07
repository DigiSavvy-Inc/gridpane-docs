# Cloudflare’s CDN and Upload Limitations | GridPane

# Cloudflare’s CDN and Upload Limitations

 

1 min read 

Cloudflare offer a great free service, and a part of that service is their CDN. This is available to all plans, including the free tier.

If, however, you are using Cloudflares CDN and are trying to upload large files to your website, you may run into an issue with their upload size (HTTP POST request size) limitations.

This is detailed in this article:https://support.cloudflare.com/hc/en-us/articles/200172516-Understanding-Cloudflare-s-CDN

Free and Pro plans are limited to a maximum upload size of 100mb.

If you need to upload files that are over 100mb in size, simply head over to your DNS page inside Cloudflare, and turn the clouds from orange to grey to turn off Cloudflare’s services:

Once these are grey you can then upload your files.

After your uploads are complete you can then turn them back to orange again.

### More on Cloudflare

If you’d like to learn more about using Cloudflare with GridPane, please check out these articles:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

