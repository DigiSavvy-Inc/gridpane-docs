# Fixing Better Uptime False Alarms | GridPane

# Fixing Better Uptime False Alarms

 

2 min read 

 

### Info

While this article is for troubleshooting Better Uptime, the advice below may also apply to other uptime monitoring solutions as most have similar feature sets.

Better Uptime is a popular uptime monitoring service within the GridPane community. Both ourselves, many of our team members, and many of our clients bought the excellent Appsumo deal in 2020.

One thing that we have experienced on rare occasions are false downtime alerts – notifications come through, but the site isn’t actually down. We recently had a client reach out to report a similar thing, and it seems that the “Timeout (no headers received)” is usually given as the reason.

Below is some advice on how to prevent them in the future.

 

## Better Uptime Settings

Consider adjusting the following settings: –

Better Uptime can also be set to where it won’t immediately alert you as soon as it spots an issue. This  could potentially greatly reduce the chances of false alarms. You may be a minute or 2 slower in your response times in cases where you have real downtime, but it also won’t interrupt your sleep or workflow unnecessarily.

This has to be configured on a per-domain basis, and you can find it under: Configure > Advanced settings.

By default it is set to immediate:

 

## Whitelisting Their IP Addresses

This probably isn’t necessary, but here is how you can whitelist their IP addresses as mentioned above.

### UFW

Whitelist in the UFW with the following command (replace “1.2.3.4” with the IP address):

```
ufw insert 1 allow from 1.2.3.4 to any
```

Blocking multiple IPs is a little more complicated with UFW and it’s probably simpler to do so one at a time.

When done, run:

```
ufw reload
```

You can check the status afterward with (though if anything is incorrect it will let you know as you do it):

```
ufw status
```

### 6G, 7G, and ModSec Firewalls

To whitelist their IP addresses in your firewall, the links below will take you to the specific section within each article:

Whitelist IPs with 6G

Whitelist IPs with 7G

Whitelist IPs with ModSec

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

