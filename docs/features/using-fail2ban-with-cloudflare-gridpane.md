# Using Fail2Ban with Cloudflare | GridPane

# Using Fail2Ban with Cloudflare

 

7 min read 

## Index

## Introduction to Fail2Ban

Huge thank you to Ken Wiesner for making this article possible and freely contributing the info to the GridPane community!

Fail2Ban is an open source intrusion detection software installed and activated by default on GridPane servers that parses system log files and automatically bans IP addresses that show signs of malicious activity for a set period of time or permanently.

The application itself is composed of three main components:

Filters define the rules by which Fail2Ban will scan local log files for bad behavior. By default, Fail2Ban comes with a library of filters for many popular software packages including SSHD, Nginx, WordPress, and more! Each filter looks for activity like too many bad login attempts, patterns of known exploits, etc.

Actions are commands that tell Fail2Ban what to do when filters are triggered. The default action in most cases is to block an offending IP address in the local firewall.

Jails consist of a filter and one or more actions to be performed.

## Using Fail2Ban with WordPress on GridPane

By using the WP fail2ban plugin, WordPress can send events to Syslog for Fail2Ban to act upon. These events include failed login attempts, spam detection, user enumeration, etc. In addition to installing and activating the plugin, we also need to set up the jails so Fail2Ban knows what to do with these events.

To make this feature robust and easy to implement, we have a GP-CLI command that will install and activate the WP fail2ban plugin as a must-use plugin and configure the necessary jail file. This is accomplished by installing the plugin in the standard plugin directory so that it will automatically update but it is activated by creating a symlink from /mu-plugins to force it to remain active.

The GP-CLI commands to enable/disable WP fail2Ban are as follows. Replace {site.url} with your site primary domain.

```
gp site {site.url} -enable-wp-fail2ban
```

```
gp site {site.url} -disable-wp-fail2ban
```

## Using an Action to block IP addresses at Cloudflare

If you are trying to use Fail2Ban when your site is behind the Cloudflare proxy, there is a problem. While the GridPane stack will automatically translate the real IP coming through Cloudflare, by default that IP address will be added to the local firewall. The problem is that it won’t do us any good if the attacker continues to be proxied through Cloudflare. The traffic from the attacker will continue to be passed from Cloudflare to the origin server because the local firewall is blocking the attacker’s IP address and not the Cloudflare IP (nor should it as this would block legitimate traffic.)

We can use a custom Fail2Ban action to send IP ban and unban requests to Cloudflare via their v4 API. This has many benefits most notable:

 

 

### Update

At the time of publishing, I had added the following code as the addition to the jail.local:
action = gpcloudflare
    iptables-multiport
It was recently brought to our attention that the integration was no longer working. The fix to get this integration back up and running is to change iptables-multiport to iptables-allports:
action = gpcloudflare
    iptables-allports

## Setting up our Action

To connect F2B and Cloudflare together we need to change the default Cloudflare configuration and add our Cloudflare API details.

### Step 1. Copy your Cloudflare API key

If you’re already using Cloudflare with your GridPane account, these are the same details in your settings page under DNS providers. It requires your Cloudflare account email address and your API key.

If you haven’t yet set Cloudflare up with your GridPane account, you can follow this guide, and it will also walk you through how to get your API key:

Using Cloudflare with GridPane

### Step 2. SSH into your server

Please see the following articles to get started:

Generate your SSH Key:

Generate SSH Key on Mac

Generate SSH Key on Windows with Putty

Generate SSH Key on Windows with Windows Subsystem for Linux

Generate SSH Key on Windows with Windows CMD/PowerShell

Add your SSH Key to GridPane:

Add default SSH Keys

Add/Remove an SSH Key to/from an Active GridPane Server

Connect to your server:

Connect to a GridPane server by SSH as Root user.

### Step 3. Update the cloudflare.conf

We’re going to update the cloudflare.conf to the latest version that solves some of the previous issues with the unban action. At the time of writing, this was updated on April 27th 2020. This is located on the F2B GitHub here:

https://github.com/fail2ban/fail2ban/blob/master/config/action.d/cloudflare.conf

Previously, I had replaced the contents of cloudflare.conf, however, let’s create a new config instead to ensure nothing gets overwritten in the future. In your server run the following command to create our new config:

```
nano /etc/fail2ban/action.d/gpcloudflare.conf
```

Now copy and paste the info from the above GitHub page to add the latest, up-to-date cloudflare.conf code.

Leave the nano editor open and move on to step 4 below to add your Cloudflare account details.

### Step 4. Add your Cloudflare details to cloudflare.conf

Still inside the gpcloudflare.conf, scroll down to the bottom of the file with your down arrow key. Here you’ll see the following:

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='0'%20height='0'%20viewBox='0%200%200%200'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/fail2ban-with-cloudflare/f2b-cloudflare-01.png)

We need to enter our API details:

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='0'%20height='0'%20viewBox='0%200%200%200'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/fail2ban-with-cloudflare/f2b-cloudflare-02.png)

Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

### Step 4. Update Jail.local

We also need to edit the jail.local file to add the Cloudflare action. To edit the file, use the following command:

```
nano /etc/fail2ban/jail.local
```

Here we need to add the following to each of our jails (make sure that iptables-multiport is tabbed over as shown in screenshot):

```
action = gpcloudflare    iptables-allports
```

You can add this at the bottom of each jail. Depending on your setup you’ll either have some or all of the following: –

Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

### Step 5. Reload Fail2Ban

Now we need to check your syntax and reload Fail2Ban for our changes to take effect:

```
fail2ban-client -d && service fail2ban restart
```

All done! Fail2Ban is now configured to work with Cloudflare.

 

### Step 6. Test your work

In my testing of this, there has been a bit of a delay between getting banned by F2B and this taking effect at Cloudflare. This means the maximum number of login attempts on a site may not work as you have configured it due to this delay.

Because of this, I’m pretty strict with my ban times, and I mention it because that may something you wish to consider as well. For testing purposes though, you may wish to keep this ban time at 2-3 minutes and then increase again afterwards. See the Configuring Fail2Ban article for details.

I recommend you test this with a VPN so as not to get your own IP banned. If not using a VPN you should definitely implement a short ban time so you can get back on to your websites ASAP.

Testing: –

1. Connect to a VPN

2. Open 2-3 of your websites that you manage in your Cloudflare account and that have orange clouds.

3. Start hitting the login button at /wp-login.php on one of the sites until you get banned:

4. Once banned, check your other websites to confirm you’re banned there too.

5. Check your Cloudflare account to confirm the ban and then to confirm that the IP is unbanned after the short period you’ve set.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

