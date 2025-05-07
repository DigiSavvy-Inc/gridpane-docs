# Suspend/Disable a Website | GridPane

# Suspend/Disable a Website

 

3 min read 

Sometimes you might need to temporarily (or otherwise) suspend/disable a client’s site. For example, this could be due to unpaid invoices, or it could be while you carry out temporary maintenance.

Whatever the use case, this is easily done on GridPane. Below will walk you through the available options.

### Table of Contents

 

 

### Info

Suspending a website via the customizer inside the dashboard is a developer only feature.

## Suspend via the Customizer

The option to disable any of your websites is available directly inside your GridPane dashboard. First, head to the Sites page within your account and click on the name of the website you would like to suspend:

Next click through to the Security tab and then the Access sub-tab. To suspend the website toggle ON. To unsuspend a website toggle OFF:

 

## Suspend via GP-CLI

To suspend via GP-CLI, you can connect to your server and run the following command (switching out site.url for your domain name):

```
gp site site.url -suspend
```

For example:

```
gp site example.com -suspend
```

 

## Example Use Case

This functionality is not just for suspending sites because clients haven’t paid, but let’s use that as an example use case.

Let’s say we have a client with the site nsfwp.club and they haven’t paid their invoice for 3 months or more, nor returned any of your calls or emails. It might be time to suspend their site…

So we run:

```
gp site nsfwp.club -suspend
```

gp-cli will create a basic html holding page on your server at /var/www/holding.html if it doesn’t already exist.

It will then copy this holding page into your site root and rename it as index.html and rename the folloing WordPress core files in root:

index.php to index.php.suspendwp-comment-post.php to wp-comment-post.php.suspendxmlrpc.php to xmlrpc.php.suspend

Then it flushes your site server cache…

Nothing overly fancy, but it does the trick:

Soon after, what do you know? Guess who has two thumbs and gets a call from their missing client?

To unsuspend their site, just run:

```
gp site nsfwp.club -unsuspend
```

 

## Customize the Suspension Page

The standard GP-CLI command will create a basic HTML file at:

```
/var/www/holding.html
```

But you might want to edit that and create your own, that’s no problem… in fact, we highly recommend that you do, and you upload the page to all your servers.

But there is more… you can also create a server custom holding template at this location:

```
/var/www/custom-holding.html
```

And run the following command to use that HTML page for your suspension page with the following command:

```
gp site site.url -suspend -use-server-custom
```

Or… perhaps you want to have a site-specific maintenance page?

Create this file:

```
/var/www/site.url/custom-holding.html
```

### Activate a Custom Holding Page

This option is not available as a toggle inside the site customizer, but you can easily activate it by running the following command like so to use that page:

```
gp site site.url -suspend -use-site-custom
```

To unsuspend your site use the following:

```
gp site site.url -unsuspend -use-site-custom
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

