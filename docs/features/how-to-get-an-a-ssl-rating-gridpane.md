# How to Get an A+ SSL Rating | GridPane

# How to Get an A+ SSL Rating

 

1 min read 

## Introduction

GridPane allows you to easily provision A+ Grade SSL certificates out of the box – nothing in our stack requires changing in order to provision.

Recently, 4 members of the GridPane community competed in the Review Signal WordPress benchmarks, each earning Top Tier honors – including the 3 who competed in the Enterprise category (check that out here).

While everyone got flying colors in everything else, 3 out of 4 participants only scored a B Grade in the Qualys SSL test. This article covers why this occurred and how to score an A+ grade.

 

 

### Information

GridPane has integrations at two DNS providers: Cloudflare and DNS Made Easy (DNSME). The information in this article only applies to Cloudflare, and DNSME does not require any settings updates out of the box to provision A+ grade SSL certificates.

## The Problem: Grade B vs A+

At GridPane, the reason for a Grade B SSL rating is due to Cloudflare (or potentially some other DNS service) supporting TLS versions older than 1.2.

The GridPane stack has already deprecated older TLS and SSL versions due to this issue. GridPane defaults to TLS 1.2 and 1.3 out of the box, however, Cloudflare offers support for 1.1 and 1.0, too, and this needs to be changed within your Cloudflare settings.

In the image above we can see the issue is due to protocol support, which we can see is due to versions below 1.2 being supported:

 

## Fixing the Issue at Cloudflare

Login to your Cloudflare account, select the domain, and then navigate to SSL/TLS > Edge Certificates. Here, you can change the Minimum TLS Version to TLS 1.2 or higher:

Now, if you provision a new SSL certificate, the rating will be A+:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

