# Snapshot Failover™ and DNS Strategy | GridPane

# Snapshot Failover™ and DNS Strategy

 

4 min read 

 

### IMPORTANT

While you technically can sync more than one source server to one failover server, we strongly recommend against this. If you do go this route, please ensure that source servers do NOT contain any of the same domains as this will cause sync issues that could affect the entire failover server.

## Intro

Snapshot Failover™ is an excellent feature to be able to offer as a part of your hosting service. It’s impressive to clients, takes relatively little effort, is relatively inexpensive if you’re taking the cost into account in your offering, and it also provides you as the service provider some peace of mind.

A second server is also a second set up backups, which is never a bad thing either.

However, an expense that can quickly add up is additional Failover records. For example, at DNS Made Easy, an extra record is $4.95 per year. That may be neither here nor there for one extra record, but if you have 100 websites, that’s an additional $495.00 per year.

CNAMEs are the solution.

 

## CNAMEs and DNS Management

We’ve already touched on how to use CNAMEs for as a part of your DNS management strategy in this article:

DNS Management and CNAMEs

You may want to read that article before proceeding if your new to managing your own DNS.

A great use case for this is WaaS networks, where you simply have all your clients point their CNAMEs towards your networks domain name, and then whenever you move your network, simply change one A record IP address, and all of your networks subsites will automatically point to the new IP address. Done and done.

You can also use this same strategy for managing sites on a server that you also want to failover to another server. Below we’ll look at an example of how to accomplish this.

 

## Step 1. Setup a subdomain

To get started, set up a subdomain with a name that makes sense for your server and the clients that you host on it. It should likely be a subdomain of your primary marketing site, and an example for a server in Atlanta (for example), maybe:

atlanta1.yourdomain.com

Another example for a server in Singapore maybe:

singapore01.yourdomain.com

Choose a subdomain that makes sense for your business and your clients, and think about your server naming conventions to come up with a naming system that makes sense for you.

 

## Step 2. Create a WordPress Site on Your Primary Server

In order for your Failover to kick in, you need a website that your failover service can monitor for downtime, so they know when to switch the A record over to the backup server.

This could be a fresh WordPress installation that remains that way forever, or it could be a simple landing page. Maybe you can even think of something creative to use as a placeholder so that if clients visit it they see something you’d specifically like them to see.

Make sure your website has DNS records set and that it is live to the world.

 

## Step 3. Setup Snapshot Failover

This is detailed thoroughly in this guide:

How to Setup Snapshot Failover™ with DNS Made Easy

In it, you will learn how to set up your failover server and activate Snapshot Failover, as well as how to setup DNS Failover records for your subdomain with DNS Made Easy. If you’re using a different DNS Failover service, the basics are still the same though the setup within your provider may differ.

 

## Step 4. Setup CNAMEs pointing to your subdomain

Now that your subdomain is up and running with Failover records, and your primary server, along with all it’s websites have been cloned over to the failover server, you can now setup your CNAMEs.

Ideally you will already be managing your clients DNS, in which case you don’t need to involve them in the process.

If not, they should be able to do this easily enough themselves if given guidance.

### Regular DNS Records

Normally, a website uses an A record with the server IP address, and a CNAME for the “WWW” record pointing towards their websites domain name. For example:

A Record: clientwebsite.com > 199.199.199.19CNAME: www > clientwebsite.com

### CNAME Strategy

Instead of the regular DNS setup, we want the client to setup two CNAMEs (and delete the existing A record if it already exists) as follows:

CNAME: clientwebsite.com > atlanta1.yourwebsite.comCNAME: www > atlanta1.yourwebsite.com

 

 

### TTL Consideration

Wherever possible, it's likely best to go with the shortest TTL that the DNS provider allows when you or your clients set up CNAMEs. The IP change will be immediate as the CNAME record isn't changing, it's the subdomain it's pointing to is changing. However, browsers may cache the IP address, and setting a short TTL will help to ensure they check for an IP change.

## Step 5. Kickback and Relax

Once all of your websites on your primary server have CNAMEs in place pointing to your subdomain, and your subdomain is being monitored for downtime, you’re all set.

If your DNS service detects that your subdomain goes down, it will automatically switch the websites IP address to point to the failover server.

As soon as that happens, all of your other websites will failover at the exact same time, as they are all are pointing towards your subdomain and therefore pointing to the same IP address.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

