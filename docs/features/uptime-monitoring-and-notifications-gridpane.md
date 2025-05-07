# Uptime Monitoring and Notifications | GridPane

# Uptime Monitoring and Notifications

 

2 min read 

### Table of Contents

 

## Introduction

Our uptime monitoring feature is available on our Developer Plus plan, and it’s available for all of your websites (not limited to 50 as per our plan during the launch of Developer Plus).

By default, this feature is turned off and must be activated on a per-website basis. This article details how our uptime monitoring works and how to turn it on and off for your sites.

 

## How GridPane Uptime Monitoring Works

### Before Activation

Upon activating uptime monitoring for a website, we’ll check that your site’s DNS is resolving to your GridPane server.

If it is NOT resolving to your server IP, we’ll then run a check for GridPane website headers.

If either of the above is in place, uptime monitoring will be activated for your website. If the site is not live on a GridPane server, you’ll receive a notification that states that activation was unsuccessful.

### Upon Successful Activation

Your website will immediately be added to our uptime monitoring system. Uptime checks will bypass your website’s cache to determine the realtime state of your website and run every minute.

To reduce false positives, when the uptime monitor registers that the site is experiencing an issue, the event is passed to a middleman to confirm the request. If both confirm the event, a notification is fired.

### Downtime Event Notifications

Notifications are sent via our support desk, which will send an email to the account holder. In these events, a ticket is created for the issue and then auto-resolved when the issue is resolved.

Please note that our team does NOT monitor for these events unless your website is enrolled in our 360 support service.

 

## Activating/Deactivating Uptime Monitoring

To activate or deactivate uptime monitoring for a website, head over to the Sites page within your account and click on the name of your website:

This will open up the website customizer, and here you will see the toggle for turning monitoring ON and OFF:

Once toggled on, the activation process will begin, and you will receive a notification on whether the operation has been successful.

When toggling off, you’ll receive a notification confirming the process has been completed once successful.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

