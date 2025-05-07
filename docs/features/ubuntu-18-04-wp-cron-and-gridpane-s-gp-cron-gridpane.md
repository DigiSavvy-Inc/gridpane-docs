# Ubuntu 18.04: WP-Cron and GridPane’s GP-Cron | GridPane

# Ubuntu 18.04: WP-Cron and GridPane’s GP-Cron

 

3 min read 

 

### Ubuntu 20.04 and 22.04 Servers

If your server is running our Ubuntu 20.04 or 22.04 stack, please see this article:
Ubuntu 20.04 & 22.04: WP-Cron and GridPane’s GP-Cron

### Table of Contents

 

## Introduction

WP-Cron is how WordPress handles scheduling time-based tasks such as checking for updates and publishing scheduled post.

At GridPane, we have GP-Cron, which does the same thing, but at the server level. Unlike WP-Cron, which relies on people visiting your website, you can set it to run at specific time intervals, ensuring that things like scheduled posts won’t miss being published.

Activating GP-Cron will disable the native WordPress cron via your websites wp-config.php file.

 

## Ubuntu 18.04 and GP-Cron

GP-Cron is NOT active by default on our Ubuntu 18.04 stack, so it needs to be manually enabled on a per-site basis.

This stack also runs our original GP-Cron, which is a straightforward cron job to trigger the WP-Cron at an interval of your choosing.

 

## Enable GP-Cron

The following will set up GP-Cron to run on your website (it is not active by default on Ubuntu 18.04 or 20.04). This command will disable WP-cron is set a server cron job:

```
gp site {site.url} -gpcron-on {minute.interval}
```

The cron will run as a system user cron for your site’s PHP user.

For example:

```
gp site yourwebsite.com -gpcron-on 15
```

The above example sets GP-Cron to run every 15 minutes.

 

## Disable GP-Cron

To disable GP-Cron you can run the following command (replace {site.url} with your website URL):

```
gp site {site.url} -gpcron-off
```

For example:

```
gp site yourwebsite.com -gpcron-off
```

 

## Checking Your Cron Job

These Cron jobs do not run under the root cron, as this would elevate WP PHP processes to root privilege and create a security risk, so you won’t find these in the regular crontab. You will need to check the website’s system user-specific crontab.

To do that you need to first move into your websites system user and display the crontab:

```
sudo su - {system.user}
```

```
crontab -l
```

{system.user} is the system user your site belongs to.

For example:

```
sudo su - steveswebs8348
```

You can also check running just one singular command as follows:

```
sudo su - {system.user} -c "crontab -l"
```

If you have run the command correctly, say for 1 minute, you should see the following in your users crontab:

```
*/1 * * * * wget -q -O - http://{your.site}/wp-cron.php?doing_wp_cron >/dev/null 2>&1
```

For more information on WP-Cron, you can check out the official documentation here:

https://developer.wordpress.org/plugins/cron/

### Return to the root user

Once done checking your cron jobs you return to the root user with CTRL+D.

 

## How to List All Sites Running GP-Cron

To view a list of all sites on a given server using GP-Cron you can run the command below to search each site’s env file for the value cron:true:

```
grep 'cron:true' /var/www/*/logs/*.env
```

Here’s an example of what the output will look like:

```
/var/www/anothergpcrontest.site/logs/anothergpcron.test.site.env:cron:true
/var/www/gpcrontest.site/logs/gpcron.test.site.env:cron:true'
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

