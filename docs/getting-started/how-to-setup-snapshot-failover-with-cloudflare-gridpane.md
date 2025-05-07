# How to Setup Snapshot Failover™ with Cloudflare | GridPane

# How to Setup Snapshot Failover™ with Cloudflare

 

7 min read 

### Table of Contents

 

## Introduction

Snapshot Failover™ is our proprietary high availability setup that allows you to clone all of the sites on one server over to another server, and set a syncing schedule for those paired servers of as little as one hour.

Couple this with automatic DNS failover that will switch your DNS records to your backup server if your primary server goes down, and you can ensure that your websites stay up and running even when your provider has an outage that impacts an entire datacenter.

This feature is available on Developer accounts.

Note: Currently Cloudflare’s free plan is not supported. The Cloudflare Load Balancing Feature which can be used for Automatic Failover starts from $5/month per site.

### How does it work?

[](https://gridpane.com/blog/snapshot-failover/?wvideo=nv7bewu2y5)

This article details how to setup Snapshot Failover works in conjunction with Cloudflare.

GridPane’s role is to do the cloning and ensure that the websites on your primary server are cloned over to your backup server, on the schedule that you set inside your dashboard.

Cloudflare’s role is to monitor your primary server and if it sees it down, automatically adjust your DNS records to point to your backup server.

 

## Part 1. Setting up Snapshot Failover™ Inside GridPane

First, navigate to the “Tools” page inside your dashboard. Snapshot Failover™ lives directly below the Self Help Tools.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='0'%20height='0'%20viewBox='0%200%200%200'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/setup-snapshot-failover/Snapshot-Failover-1.jpg)

Here we need to set the source server, failover server and sync interval.

Once you’ve set the details, click the “Sync Servers” button.

 

## Part 2: Setting Up Cloudflare Load Balancing

Cloudflare operates a little differently to DNSME and doesn’t have a specific “Failover” feature.

Instead, Cloudflare has a load balancing feature that will allow us to create our own failover. Below we’ll be configuring load balancing specifically for this purpose.

We do this by creating what are called “Pools”.

A Cloudflare Load Balancing pool usually represents a group of origin servers, but in our case, one pool will contain our primary source server (Primary-Pool), and the second will contain our backup failover server (Failover-Pool). We’ll set up Cloudflare so that it drives all traffic to the Primary-Pool, and if it finds that this is unhealthy or not responsive, it will change our domains A record to point to our Failover-Pool.

This is called Active Failover. More details can be found here:

https://developers.cloudflare.com/load-balancing/reference/common-configurations

 

### Step 1: Setup Load Balancing

To create a load balancer, click through to your website inside your Cloudflare account, and then through to the Load Balancing inside the Cloudflare Traffic tab.

Load balancing is a paid feature and has to be able enabled before proceeding.

You’ll be asked to confirm your subscription or enter your payment details before activation:

When load balancing is enabled, you’ll see these 3 options as blue buttons:

The following steps are technically the most efficient if this is your first time setting up a load balancer.

 

### Step 2: Create 2 monitors

Click the Manage Monitors button to begin setting up your health monitors.

To ensure your monitor is able to accurately detect whether your site is healthy or not, the following is how you may want to configure these settings, but feel free to adjust as you see fit:

Click “Save” when ready, and then repeat the process to create a second monitor for our Failover site.

 

### Step 3: Create a primary pool and a failover pool

Back on the main Load Balancing page, click the “Manage Pools” button, and then click the “Create” button in the Origin Pools page.

Your primary source server will be used for your Origin Pool in your load balancer.

Important: If you don’t set a host header Cloudflare will not be able to properly monitor the health of your site.

You can skip past the follow settings:

Next:

And finally, enter an email address for where you wish to receive notifications about the health of this server.

Click Save to finish up.

###### Create a Secondary Pool

Now we need to add another pool for our failover. Repeat all of the above to add your failover server (and it’s correct IP address).

 

### Step 4.1: Create Your Load Balancer

Back on the Load Balancer main page, click the “Create a Load Balancer” button.

 

### Step 4.2: Set Your Hostname

Your hostname is either your root domain (e.g. yourdomain.com) or a subdomain (sub.yourdomain.com), depending on your site URL. Here you can also choose whether your traffic is proxied or not.

When configured click Next.

 

### Step 4.3. Set Your Origin and Failover Pools

From the dropdown, select your primary server and add it as your origin pool:

Then set your Failover pool.

Click Next.

 

### Step 4.4. Confirm Your Monitor

The monitor for your origin pool should already have been attached to it in Step 3, but if it isn’t you can set it now. Also, be sure to go to your Failover pool and set the failover monitor so that you’re alerted should it ever go down.

 

### Step 4.5. Traffic Steering

Traffic steering should be set to off. This is what we need for failover to function.

With this turned off, all traffic will be routed to the primary server unless it fails a health check, in which case it will then be routed to our failover server.

 

### Step 4.6. Custom rules

Set them if you want them, but feel free to skip.

 

### Step 4.7. Review and Deploy

Before completing the creation of your new load balancer, CloudFlare will display a summary of your configuration so that you can review and confirm your settings (and make any changes if necessary).

Once you’re satisfied, click “Save and deploy” and your load balancer will immediately go live (or save as a draft if you’re not yet ready to set it live).

You’ve now completed your Snapshot Failover setup.

 

## Learn More About Cloudflare Load Balancers

The following articles directly from Cloudflare provide an overview of their load balancing suite of tools:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

