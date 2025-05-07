# My website has encountered a critical error or looks broken, what do I do? | GridPane

# My website has encountered a critical error or looks broken, what do I do?

 

1 min read 

Sometimes a plugin or other component of your website misbehaves and triggers a critical error, or if you haven’t configured Nginx Helper but are using server cache it will make your site appear broken.

If you have email set up on your website, review the email that WordPress sent you, it can contain a lot of valuable information. If you don’t have that, proceed to the following troubleshooting steps:

## Step 1: Disable Caching

Disable all server caching, any external caching (Cloudflare, etc), do a full cache clear via Tools > Quick Fix > Clear All Nginx Caches. Review the error logs in the Site Customizer (click on the domain to launch it):

Once you review the error, it may guide you as to which plugin or component is throwing an error. If it doesn’t solve the issue, proceed to Step 2.

## Step 2: Disable all plugins

If the error goes away, then it’ll be one or more plugins conflicting. Enable plugins one at a time until the culprit is discovered. If this doesn’t help, proceed to Step 3.

## Step 3: Change the theme

Change the theme to the regular vanilla theme. If that doesn’t help, proceed to Step 4.

## Step 4: Change PHP version

It may be that a plugin needs an older version of PHP. Also do a WPCLI database check.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

