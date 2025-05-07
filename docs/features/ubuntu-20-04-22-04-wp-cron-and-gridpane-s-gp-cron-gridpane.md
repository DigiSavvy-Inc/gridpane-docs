# Ubuntu 20.04 & 22.04: WP-Cron and GridPane’s GP-Cron | GridPane

# Ubuntu 20.04 & 22.04: WP-Cron and GridPane’s GP-Cron

 

11 min read 

### Table of Contents

 

## Introduction

WP-Cron is how WordPress handles scheduling time-based tasks such as checking for updates and publishing scheduled post.

At GridPane, we have GP-Cron, which does the same thing, but instead triggers the cron at the server level. Unlike WP-Cron, which relies on people visiting your website, you can set it to run at specific time intervals, ensuring that things like scheduled posts won’t miss being published.

Activating GP-Cron will disable the native WordPress cron via your website’s wp-config.php file.

### Quick Activation/Customization

This article covers how GP-Cron works and all the available options. However, if you simply need to turn GP-Cron on for a website or change the interval, please see this section:

Simple GP-Cron Activation ▼

 

Part 1: GP-Cron Functionality

 

## Ubuntu 20.04 and GP-Cron

GP-Cron is NOT active by default on our Ubuntu 20.04 stack, so it needs to be manually enabled on a per-site basis. However, its functionality has been significantly upgraded and brought in line with the newer functions initially developed for our newer Ubuntu 22.04 stack (more info below).

### 20.04 Stack Nuances

The WP-CLI type cron was previously only used by the 22.04 stack, but this has now also been to the Ubuntu 20.04 stack as of Feb 23rd 2024. However, we have not retroactively update any existing GP server crons that you have set up yourself prior to this.

As you likely have GP-Cron running on far fewer websites than on 22.04 servers, it should not be necessary to update these yourself unless you wish to do so. If you do want to update existing crons to the new standard, simply run the enable command again and the function will update the old cron to the new.

### Functions that will auto-update your previous crons

Functions that interact with the crons will now update any old crons you’ve set to the new crons. These are:

If any of these are run on a site with an existing legacy cron, the cron will be updated.

 

## Ubuntu 22.04+ and GP-Cron

On Ubuntu 22.04 and all future stacks, GP-Cron is now active by default for all of your sites.

This is automatically configured to run every 5 minutes out of the box with our default “fuzziness” configuration active. More information can be found on this below, but in a nutshell, this is our method for randomising the times that GP-Cron runs to prevent CPU spikes.

If you would like to change the frequency of your cron jobs, or deactivate GP-Cron for one or more sites, you can follow the steps in this article.

 

## GP-Cron Improvements

We’ve introduced additional improvements/updates to GP-Cron, and these are now included in our 20.04 stack and 22.04 stack. These improvements include:

 

### GP-Cron Timing, Format, and Logging

 

 

### Feb 2024 Update

This section details new functionality introduced on February 23rd 2024.

Default cron does not have its own randomizer or “fuzzy” configuration. This means that it can only be set on a per-minute basis. For servers that have higher tenancy rates (meaning they host a lot of sites), this can result in many cron jobs triggering at the same time, which could spike CPU load on smaller servers.

To prevent this, we have introduced two options:

The formatting for the cron jobs created has also been altered accordingly, and we’ve added additional logging for debug purposes. 

Part 2: Configure GP-Cron

 

## Activating/Customizing GP-Cron

The following commands can be used to activate and/or customize the timing of GP-Cron on your websites. To configure GP-Cron, you will need to SSH into your server. If this is your first time connecting to your server, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Command Syntax

The following command can be used to activate GP-Cron, or customize the existing cron job:

```
gp site {site.url} -gpcron-on {minute.interval} -fuzziness/-sec-delay {integer.seconds}
```

The two flags -fuzziness and -sec-delay are optional. These flags are also mutually exclusive and so cannot be used together. This means it’s either:

```
gp site {sites.url} -gpcron-on {integer.minutes} -fuzziness {integer.seconds}
```

Or:

```
gp site {sites.url} -gpcron-on {integer.minutes} -sec-delay {integer.seconds}
```

If used together the -fuzziness will be used and the  -sec-delay flag will be ignored.

### Default Configuration

Here’s an example of how the command looks (and this is also our default configuration):

```
gp site site.com -gpcron-on 5 -fuzziness 270
```

 

## Option 1: Simple GP-Cron Activation

The following command can be used to activate and/or change the time interval for GP-Cron – switch out {site.url} for your website URL and {minute.interval} for your desired interval:

```
gp site {site.url} -gpcron-on {minute.interval}
```

For example:

```
gp site gridpane.com -gpcron-on 15
```

The above example sets GP-Cron time to every 15 minutes and uses our default fuzziness value.

 

## Option 2: Configure GP-Cron “Fuzziness”

The aim of our fuzziness configuration is to spread the intervals across the entire time frame on the server, preventing CPU spikes from multiple cron jobs triggering at the exact same time.

### How it works

Fuzziness works by randomizing when each crons will execute within the time period set on a per site basis.

We also leave a 30-second buffer around each interval so that there will always be a minimum of 30 seconds between possible cron jobs running.

This all means that each website running our default 5-minute configuration will trigger at a random time between 1 second and 4 minutes and 30 seconds at each interval, and crons will always trigger twice within 10 minutes (2 intervals), but may mean two crons may be more or less than 5 minutes apart from each other.

### GP-Cron 22.04 Default Setting

The GP-Cron default for all websites on Ubuntu 22.04 servers is as follows:

Which is the same as running:

```
gp site site.url -gpcron-on
```

```
gp site site.url -gpcron-on 5 -fuzziness 270
```

This default is also our maximum possible fuzziness for a 5-minute cron.

### Maximum Fuzziness Setting

We will only accept fuzzy second values based on this formula:

```
max_fuzzy_seconds=$((minute_freq * 60 - 30))
```

For example:

### Turn Fuzziness Off

If you require that one or more sites are strictly regular you can set the following:

```
-gpcron-on 3 -fuzziness 0
```

Setting the fuzziness to 0 will trigger the cron job on the dot at every interval.

 

## Option 3: Configure GP-Cron with a Custom Sec-Delay

While our fuzziness configuration is great for most use cases, we also have our custom delay flag “-sec-delay” which offers the ability to set crons at an exact interval.

The command is as follows – you’ll need to replace {site.url} with your website URL, {integer.minutes} with your desired cron frequency, and {second.interval} with your delay period:

```
gp site {sites.url} -gpcron-on {integer.minutes} -sec-delay {integer.seconds}
```

For example, if you have 10 sites on a server and they all need an exact regular 2-minute interval, you could set them up as follows:

```
gp site one.com -gpcron-on 2 -sec-delay 0
gp site two.com -gpcron-on 2 -sec-delay 10
gp site three.com -gpcron-on 2 -sec-delay 20
gp site four.com -gpcron-on 2 -sec-delay 30
gp site five.com -gpcron-on 2 -sec-delay 40
gp site six.com -gpcron-on 2 -sec-delay 50
gp site seven.com -gpcron-on 2 -sec-delay 60
gp site eight.com -gpcron-on 2 -sec-delay 70
gp site nine.com -gpcron-on 2 -sec-delay 80
gp site ten.com -gpcron-on 2 -sec-delay 90
```

This provides a 10-second interval between each cron job, and so the above would create the following schedule:

```
*/2 * * * * user1 sleep 0;
*/2 * * * * user2 sleep 10;
*/2 * * * * user3 sleep 20;
*/2 * * * * user4 sleep 30;
*/2 * * * * user5 sleep 40;
*/2 * * * * user6 sleep 50;
*/2 * * * * user7 sleep 60;
*/2 * * * * user8 sleep 70;
*/2 * * * * user9 sleep 80;
*/2 * * * * user10 sleep 90;
```

### Maximum Allowed Delays

You can set sec-delays based on this formula:

```
max_sec_delay=$((minute_freq * 60 - 1))
```

This means you can set delays to cover the entire period but restricts crons from mistakenly overlapping.

For example, for a 3 minute frequency would work as follows: 3 x 60 = 180 seconds. 180 – 1 = a maximum delay of 179 seconds.

If you try to set something beyond this range, it will be refused and fall back to our default fuzziness.

 

## Disable GP-Cron

To disable GP-Cron you can run the following command (replace {site.url} with your website URL):

```
gp site {site.url} -gpcron-off
```

For example:

```
gp site gridpane.com -gpcron-off
```

 

Part 3: Additional Notes

 

## GP-Cron Format Before and After

The crons have been adapted from:

```
*/5 * * * * xxx /bin/date >>/home/xxx/home/xxx/sites/xxx/logs/gp-cron.log; /usr/local/bin/wp cron event run --due-now --path=/var/www/xxx/htdocs >>/home/xxx/home/xxx/sites/xxx/logs/gp-cron.log 2>1
```

To now be:

```
*/5 * * * * xxx sleep $(/usr/local/bin/lib/randomish.sh 270); echo "$(/bin/date) >>> >>> >>> >>>" >>/home/xxx/home/xxx/sites/xxx/logs/gp-cron.log; /usr/local/bin/wp cron event run --due-now --path=/var/www/xxx/htdocs >>/home/xxx/home/xxx/sites/xxx/logs/gp-cron.log 2>&1; echo "$(/in/date) <<< <<< <<< END" >>/home/xxx/home/xxx/sites/x/logs/gp-cron.log
```

This includes the extra date logging at the end of the cron log for debug purposes, but the main thing is the addition of the randomish.sh script:

```
sleep $(/usr/local/bin/lib/randomish.sh 299)
```

 

## Checking Your Cron Jobs

GP-Cron jobs are now located in /etc/cron.d. The GP-cron file naming convention replaces . with -. For example:

To view your cronjob, you can use the above naming convention in combination with this command:

```
cat /etc/cron.d/gp-cron-site-url
```

For example:

```
cat /etc/cron.d/gp-cron-yourwebsite-com
```

 

## Checking Your Old Cron Jobs on Ubuntu 20.04 (Set before Feb 23rd 2024)

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

