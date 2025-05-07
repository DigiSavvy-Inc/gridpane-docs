# Site Firewalls: 6G | GridPane

# Site Firewalls: 6G

 

1 min read 

The 6G WAF was originally developed by Jeff Starr at Perishable Press for Apache-based servers.

6G is an excellent lightweight firewall that parses requests for anything anomalous or malicious looking, looking for:

We have adapted the firewall for Nginx, but more details can be found here.

Logging, working with rulesets and whitelisting information can be found here.

### Turn on 6G WAF

Enable the 6G firewall where {site.url} is your WordPress site’s primary domain.

```
gp site {site.url} -6g-on
```

### Turn off 6G WAF

Disable the 6G firewall where {site.url} is your WordPress site’s primary domain.

```
gp site {site.url} -6g-off
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

