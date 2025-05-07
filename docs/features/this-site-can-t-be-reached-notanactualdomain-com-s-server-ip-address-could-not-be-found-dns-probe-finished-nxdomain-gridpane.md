# This site can’t be reached notanactualdomain.com’s server IP address could not be found. DNS_PROBE_FINISHED_NXDOMAIN | GridPane

# This site can’t be reached notanactualdomain.com’s server IP address could not be found. DNS_PROBE_FINISHED_NXDOMAIN

 

1 min read 

When you received this error, it typically means that you haven’t added an A record for the domain you’re trying to reach, or that it hasn’t propagated yet.

First check your DNS records to make sure that they are all in place and live worldwide. You can use this website to check your A and CNAME records, where they point to, and where they are live in the world:

https://dnschecker.org/#A

If your records have not yet been set, you can learn more about setting DNS records here:

Setting DNS Records

Also, if you’re adding a wildcard record, please also ensure that you have the standard A record for the root domain in place as well.

For reference, this is what the screen looks like:

### Known issues

At Namecheap, even if you have the DNS right, it will sometimes not propagate until you re-add a root A record as an @ sign instead of the domain name. We’re not quite sure why that happens, but we’ve noticed it with several Namecheap customers.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

