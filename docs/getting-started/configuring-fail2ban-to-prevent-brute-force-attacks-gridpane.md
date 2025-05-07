# Configuring Fail2Ban to Prevent Brute Force Attacks | GridPane

# Configuring Fail2Ban to Prevent Brute Force Attacks

 

16 min read 

### Table of Contents

Introduction

Part 1. Use GP-CLI to Configure Fail2Ban for Strict Brute Force Protection

Part 2. Use the WP Fail2Ban Plugin Integration

Part 3. Whitelisting IP Addresses

Part 4. Manually Banning an IP Address

Part 5. Unbanning an IP Address and Checking if an IP is Banned

Part 6. Configuring the [sshd] Jail

Part 7. Fail2Ban Syntax Check

Part 8. Fail2Ban Activity Log

 

## Introduction

Fail2Ban is an intrusion prevention software framework that’s highly effective at preventing brute-force attacks. It is enabled on all GridPane servers and is protecting the SSH port by default. In this article, we’ll look at how to configure it for stricter brute force and spam protection of WordPress installations.

 

 

### Important

There are two parts to this article. Both are completely independent from one another, and neither is required for the other to function correctly. You can choose to use either Part 1 or Part 2, or both.

### Part 1: Securing the WP Login Page and XMLRPC with GP-CLI

This details how to add an extra layer of server security by setting up strict jails monitoring the Nginx access logs for wp-login.php and xmlrpc.phprequests. This will work for ALL WordPress installations on your server and protect them against brute force attacks and will automatically ban IP addresses after X number of attempts for X amount of time – configurable to your requirements.

### Part 2: Setting Up the wp Fail2Ban WordPress Plugin

This details our auto-configuring integration with the WP Fail2Ban plugin, which you can install on an individual site by site basis. This allows you to set up even further protection across a wide range of WordPress features such as comments, pingbacks, logins, etc, and it also integrates with WP logging. This means that when you mark a comment as spam, Fail2Ban will see this and ban that IP.

These are both independent from one another. You do not need to activate the plugin for the server level brute force protection to work.

### Disabling XML RPC

XML RPC is an old, outdated, and insecure method of remotely posting to your WordPress website. There are still a few plugins such as Jetpack that still use it (Jetpack has its own brute force protection option available), but for most websites, it’s simply not needed.

Before we get started, if you’re not using XML RPC on your website, then you can disable it completely with:

```
gp site {site.url} -disable-xmlrpc
```

Switch {site.url} with your domain of course, and the same goes for all of the commands that follow below.

Example:

```
gp site gridpane.com -disable-xmlrpc
```

Note: We also have other GP-CLI commands to harden Nginx for WordPress further here.

### Cloudflare, Stackpath, & Sucuri

GridPane has real IP’s configured via the ngx_http_realip_module for Cloudflare, Stackpath, and Sucuri. This allows our integration with Fail2Ban to work correctly with each of these CDN’s.

 

 

### Info

These GP-CLI commands will auto-restart Fail2Ban when enabled, and they will also ensure that Fail2Ban reload is triggered when any new WordPress site is added so that the new site logs are monitored immediately.

### Connecting to Your Server

While the security tab allows the activation of the WP Fail2Ban plugin on your individual websites, and has toggles for each of its different functions, some of this article requires connecting to your server.

To follow along with Part 1 of this article, and for whitelisting an IP address in part 2, you’ll first need to SSH into your server. Please see the following guides to get started.

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2116'%20height='940'%20viewBox='0%200%202116%20940'%3E%3C/svg%3E)

## Part 1. Use GP-CLI to Configure Fail2Ban for Strict Brute Force Protection

The following GP-CLI commands will allow you to create strict rules for wp-login.php and xmlrpc.php on all of the websites on your server. Each can be configured individually.

### Step 1. Setup a custom rule and jail for wp-login.php

The following command will create our rule and jail:

```
gp stack -enable-fail2ban-jail wp-login {retry.int} {duration.seconds}
```

Using the {retry.int} and {duration.seconds} parts of the above command sets 2 important rules that we can modify to suit our needs:

This is what the command looks like when setting the login attempts to 5 and ban time to 1200s:

```
gp stack -enable-fail2ban-jail wp-login 5 1200
```

You can adjust these 2 settings as needed. For example, 5 login attempts may be too strict for your needs, and/or 20 minutes may not be long enough.

You can set these accordingly, and here’s a handy link for converting minutes/hours into seconds:http://unitconverter.io/minutes/seconds/20

To disable this on your server, you can use the following command:

```
gp stack -disable-fail2ban-jail wp-login
```

NOTE: If you’re setting zero tolerance type rules on client sites, you may want to let them know about the extra security and to be careful when typing out their username and passwords.

### Step 2. Setup a custom rule and jail for xmlrpc.php

Now we’ll configure the rules for xmlrpc following the same guidelines as above. The command is:

```
gp stack -enable-fail2ban-jail xmlrpc {retry.int} {duration.seconds}
```

Configure the retry interval and duration as you require. You can also disable it at any time with:

```
gp stack -disable-fail2ban-jail xmlrpc
```

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='800'%20height='355'%20viewBox='0%200%20800%20355'%3E%3C/svg%3E)![](https://gridpane.com/wp-content/uploads/2020/04/f2b-part2.1.jpg) 

## Part 2. Use the WP Fail2Ban Plugin Integration

Below we’re going to install and configure the WP Fail2Ban plugin. The commands detailed in part 1 are completely independent from the UI toggles/commands detailed here in part 2.

Before we begin, there’s a couple of things we need to quickly cover as it has the potential to be confusing.

Activating WP Fail2Ban inside your GridPane account, or by running the GP-CLI commands below will  install the WP Fail2Ban plugin in your websites plugins folder but it has its main file symlinked into the Must Use plugins directory:

```
../{site.url}/htdocs/wp-content/mu-plugins
```

This means that inside your WordPress website the plugin will appear as inactive on the plugins page, but active on the must use plugins page: wp-admin/plugins.php?plugin_status=mustuse

We do this because WP Fail2Ban is a security plugin and automatic updates are important for it. However, we manage it via GP-CLI which updates the wp-config.php file with constants and sets the Fail2Ban jails and configurations needed on the server, so it is important for it to be a MU plugin.

Unfortunately, MU plugins can’t be auto-updated by WordPress core, so instead, we keep the plugin files in the standard directory, which allows the WP core functionality to auto-update it. For this reason, if your clients have Administrator privileges, you may wish to keep them informed about the special status of this plugin.

WP Fail2ban integrates WordPress logging with the syslog allowing the Fail2Ban firewall to automate the banning of IPs based on requests to WordPress.

 

### Enabling/Disabling Fail2Ban integration with WP Fail2Ban

To enable or disable the WP Fail2Ban integration for your WordPress site you simply need to head to the Sites page inside your GridPane account, click on your website to open up the configuration modal, and you will see the option inside the security tab:

You can also activate via GP-CLI with the following commands (and then hit the sync button shown above to sync it up with the server):

```
gp site {site.url} -enable-wp-fail2bangp site {site.url} -disable-wp-fail2ban
```

This will reconfigure your wp-config.php to include the following additional file:

```
/var/www/{site.url}/wp-fail2ban-configs.php
```

Within this new configuration file you will find the following constant definitions required by the plugin:

```
define('WP_FAIL2BAN_BLOCK_USER_ENUMERATION', true);define('WP_FAIL2BAN_BLOCKED_USERS', [ 'admin','Admin','user','User','user1','User1','Administrator','administrator','demo','Demo' ]);define('WP_FAIL2BAN_LOG_COMMENTS', true);define('WP_FAIL2BAN_LOG_COMMENTS_EXTRA', 0x00020002 | 0x00020004 | 0x00020010);define('WP_FAIL2BAN_LOG_PASSWORD_REQUEST', true);define('WP_FAIL2BAN_LOG_PINGBACKS', true);define('WP_FAIL2BAN_LOG_SPAM', true);
```

These constants are used by the plugin to enable, disable, and configure each of its monitoring integrations.

All are activated by default and you can use the toggles inside the UI or the commands that follow below to turn them on and off as needed.

 

### Blocking User Enumeration

This is the primary brute force protection option. Brute forcing WordPress requires knowing a valid username which isn’t particularly difficult in most cases. This will block bots during the process of gathering this information before they have a chance to do anything else. The following GP CLI command turns on this feature:

```
gp site {site.url} -configure-wp-fail2ban -block-user-enumeration
```

And this command turns it off:

```
gp site {site.url} -configure-wp-fail2ban -unblock-user-enumeration
```

 

### Block Stupid Usernames

If a common, insecure username is used in a login attempt, Fail2Ban will block this IP.

The following GP CLI command turns on this feature:

```
gp site {site.url} -configure-wp-fail2ban -block-stupid-usernames
```

And this command turns it off:

```
gp site {site.url} -configure-wp-fail2ban -unblock-stupid-usernames
```

The WP Fail2Ban integration blocks the following usernames by default:

If you currently use any of these usernames, we highly recommend that replace them with more secure alternatives. However, if they are important to you, please disable this block or adjust the constant that defines this array.

These usernames are defined in an array within the following constant.

```
define('WP_FAIL2BAN_BLOCKED_USERS', [ 'admin','Admin','user','User','user1','User1','Administrator','administrator','demo','Demo' ]);
```

This can be adjusted in the following file:

```
/var/www/{site.url}/wp-fail2ban-configs.php
```

Please be aware, enabling or disabling this feature will reset the array back to default.

 

### Guard Comments

Enabling this will allow Fail2Ban to automatically block comment attempts from banned IP addresses.

The following GP CLI command turns on this feature:

```
gp site {site.url} -configure-wp-fail2ban -guard-comments
```

And this command turns it off:

```
gp site {site.url} -configure-wp-fail2ban -unguard-comments
```

 

### Guard Password Resets

Enabling this will allow Fail2Ban to log password reset attempts and block any attempts from previously banned IP addresses.

The following GP CLI command turns on this feature:

```
gp site {site.url} -configure-wp-fail2ban -guard-password-resets
```

And this command turns it off:

```
gp site {site.url} -configure-wp-fail2ban -unguard-password-resets
```

 

### Guard Pingbacks

Enabling this will allow Fail2Ban to log and ban failed pingback attempts.

The following GP CLI command turns on this feature:

```
gp site {site.url} -configure-wp-fail2ban -guard-pingbacks
```

And this command turns it off:

```
gp site {site.url} -configure-wp-fail2ban -unguard-pingbacks
```

 

### Guard Against Spam

By enabling this, any comments you mark as spam will be banned by Fail2Ban.

The following GP CLI command turns on this feature:

```
gp site {site.url} -configure-wp-fail2ban -guard-spam
```

And this command turns it off:

```
gp site {site.url} -configure-wp-fail2ban -unguard-spam
```

 

## Part 3. Whitelisting IP Addresses

To whitelist an IP address, you’ll first need to SSH into your server. Please see the guides listed earlier in the article to get started.

Once on your server, run the following command to open up the jail.local file in the nano editor:

```
nano /etc/fail2ban/jail.local
```

Here you will see blocks that looks as follows:

```
[wordpress-wp-login]enabled = trueport = http,httpsfilter = wordpress-wp-loginlogpath = /var/log/nginx/*access.logmaxretry = 5bantime = 1200ignoreip =
```

Depending on what jails you have active, you may see anywhere from 1-5 of the following jails: –

To whitelist an IP address you will need to add a new lines as follows at the bottom of each block:

```
ignoreip = 127.0.0.1
```

You can add more than one IP by separating them with a space:

```
ignoreip = 127.0.0.1 123.456.789.01
```

You can also a whole IP block like this

```
ignoreip = 127.0.0.1 123.456.789.01 987.654.321.012/24
```

So, the blocks will each look similar to this:

```
[wordpress-hard]filter = wordpress-hardlogpath = /var/log/auth.logmaxretry = 1port = http,httpsignoreip = 127.0.0.1 123.456.789.01 987.654.321.012/24
```

Make sure you add this to each jail, otherwise this IP still may end up getting banned.

Once that’s set, hit CTRL+O and then Enter to save the file. Exit nano with CTRL+X.

We now just need to check the syntax is OK and restart Fail2Ban:

```
fail2ban-client -d && service fail2ban restart
```

And you should be all set!

 

## Part 4. Manually Banning an IP Address

You can manually ban an IP address directly on the server. Run the following command, replacing the actual IP address:

```
fail2ban-client set wordpress-extra banip {ip-address}
```

You can change the jail if you wish to do so, but the ban time for the wordpress-extra jail is 24 hours (86400 seconds). You can find each of the 5 jail names listed in part 3 above, and you could also create your own jail.

For example:

```
fail2ban-client set wordpress-extra banip 199.199.199.199
```

 

## Part 5. Unban an IP Address and Checking if an IP is Banned

### Check if an IP is Banned

If you’re not sure if your IP address has been banned or which jail it has been banned in, you can run the following command:

```
zgrep {ip-address} /var/log/fail2ban.log*
```

For example:

```
zgrep 199.199.199.199 /var/log/fail2ban.log*
```

Here, if you are banned, you’ll see something like as follows, containing the jail in which this IP is banned:

```
2021-01-01 20:20:11,121 fail2ban.actions [15591]: NOTICE [wordpress-wp-login] Ban 199.199.199.199
```

### Unban an IP

Unbanning an IP address is straightforward. Run the following command, replacing {jail-name} with the jail that banned you {ip-address} with your actual IP address:

```
fail2ban-client set {jail-name} unbanip {ip-address}
```

You can find each of the 5 jail names listed in part 3 above.

For example:

```
fail2ban-client set wordpress-wp-login unbanip 199.199.199.199
```

 

## Part 6. Configuring the [sshd] Jail

We leave the [sshd] jail with the default ban time of 10 minutes. If you’d like to enforce a stricter, longer ban time, you can add the following block to the jail.local file.

First, edit the file with nano:

```
nano /etc/fail2ban/jail.local
```

Add the following:

```
[sshd]
enabled = true
banaction = iptables-multiport
maxretry = 10
findtime = 43200
bantime = 86400
```

Change the ban time to your desired length. The time is in seconds.

Save the file with CTRL+O followed by Enter. CTRL+X to exit nano.

Next, move on to Part 6 below to check and reload Fail2Ban.

 

## Part 7. Fail2Ban Syntax Check

If you’re implementing your own custom changes and you need to check Fail2Ban’s syntax, you can run the following command:

```
fail2ban-client -d
```

If your syntax is correct, the output may quite along.

An incorrect syntax will look similar to this:

```
root@yourservername:~# fail2ban-client -dFailed during configuration: File contains no section headers.file: '/etc/fail2ban/jail.local', line: 6'utyjrykjtuiyktyui[wordpress-hard]\n'ERROR: The configuration stream failed because of the invalid syntax.Init of command line failedroot@yourservername:~#
```

You will need to fix whatever is causing the syntax failure before loading any changes.

Once fixed, you run a final syntax check and restart Fail2Ban with:

```
fail2ban-client -d && service fail2ban restart
```

 

## Part 8. Fail2Ban Activity Log

All Fail2Ban related events are logged in the fail2ban.log. Here you can check on IPs that have been banned/unbanned. You’ll notice a lot of “Found”, which means these IPs are logged, but not exceeding the thresholds for bad behaviour that result in an actual ban.

The log is available directly inside your GridPane account. To view it, head to your Servers page, and click on the desired server to open up the configuration modal. The log can be found inside the logs tab as shown below:

Server LocationThe log can be found here when accessing your server via SSH or SFTP as the Root user:

```
/var/log/fail2ban.log
```

 

 

### Legacy Note

The section below is from our previous article before the GP-CLI detailed in part 1 was created. Manual configurations of Fail2Ban can be created at a user's discretion and will require a reload of Fail2Ban whenever a new site is added to your server. We've left this here for reference/learning material, but you're better off using the steps in part 1.

## Reference: Manually Configure a Fail2Ban Jail for WordPress

### Step 1. Setup a custom wp-login.conf

First, create the file wp-login.conf with the following command, you can call this conf file anything you like as long as the jail has a value that corresponds with its naming convention:

```
nano /etc/fail2ban/filter.d/wp-login.conf
```

Inside the file, paste the following:

```
[Definition]
failregex =  [0-9].[0-9]{3} - .* "POST //wp-login.php .* 200
  [0-9].[0-9]{3} - .* "POST /wp-login.php .* 200
  [0-9].[0-9]{3} - .* "POST //xmlrpc.php .* 200
  [0-9].[0-9]{3} - .* "POST /xmlrpc.php .* 200
ignoreregex =
datepattern=%%d/%%b/%%Y:%%H:%%M:%%S %%z
```

Now Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

Your wp-login.conf is now set up, next we configure the jail.

### Step 2. Create the jail and set the rules

Now we’ll configure the jail rules by modifying the /etc/fail2ban/jail.d/defaults-debian.conf:

```
nano /etc/fail2ban/jail.d/defaults-debian.conf
```

Or, alternatively, you can create a jail.local file here instead and add your jail rules here with:

```
nano /etc/fail2ban/jail.d/jail.local
```

Please choose one or the other, not both.

Add the following block to the end of the file:

```
[wp-login]
enabled = true
logpath = /var/log/nginx/*access.log
filter = wp-login
bantime = 1200
findtime = 60
ignoreip =
maxretry = 5
```

Now Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

The above sets 2 important rules that we can modify to suit our needs:

You can adjust these 2 settings as needed. For example, 5 login attempts may be too strict for your needs, and/or 20 minutes may not be long enough.

You can set these accordingly, and here’s a handy link for converting minutes/hours into seconds:http://unitconverter.io/minutes/seconds/20

###### A Note on Jail Names

Fail2Ban jail names are restricted by the iptables max name length of 29 characters, and Fail2Ban uses a “f2b-” prefix, which further reduces your allowable name length to be a maximum of 25 characters.

If your jail name exceeds this, you’ll see a notice in the log like this when the reloading Fail2Ban and your jail will not work correctly:

```
2022-01-21 17:09:50,981 fail2ban.jail  [3491]: WARNING Jail name 'wordpress-extra-extra-extra-extra-extra' might be too long and some commands might not function correctly. Please shorten
```

### Step 3. Reload Fail2Ban

You will need to check your syntax and reload Fail2Ban.

```
fail2ban-client -d &&
service fail2ban restart
```

If you manually configured your fail2ban jails, you will need to reload Fail2Ban after you add any additional new site to ensure the new site logs are picked up and monitored immediately.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

