# Why Do You Schedule Server Restarts? | GridPane

# Why Do You Schedule Server Restarts?

 

2 min read 

If you’ve received a notification that a server restart has been scheduled, the reason will be that new security updates are now available.

We push all new security updates within 24 hours of them being released. If a reboot is needed for these updates to take effect, Unattended Upgrades schedules this for the following 02.30 UTC time slot. The process is automatic, and the reboot only takes about 30-60 seconds on average.

 

 

### Info

Settings for the configuration of unattended upgrades is now available in the UI. This includes setting times for reboots and the ability to disable automatic reboots.

## Adjust Your Timezone

If you’d like to change your server’s timezone so that they take place at a time more convenient for your websites/clients, this article will walk you through the process:

How to Change Your Servers Time Zone and Automatic Security Reboot Time

 

## Turning Off/Configuring Automatic Updates

We recommend that you leave automatic updates on. The downtime from such reboots are minimal, and this ensures that your servers are kept up to date with the latest security patches.

However, if you wish to run security updates yourself, or want to take control over how and when they are pushed, the above article will also walk you through how to do so.

 

## Legacy

### Edit the Unattended Upgrades Settings

First, SSH into your server, and then open up the unattended upgrades settings configuration with nano as follows:

```
nano /etc/apt/apt.conf.d/50unattended-upgrades
```

You will see the following two settings a little over half way down:

```
// Automatically reboot *WITHOUT CONFIRMATION*
//  if the file /var/run/reboot-required is found after the upgrade
Unattended-Upgrade::Automatic-Reboot "true";

// If automatic reboot is enabled and needed, reboot at the specific
// time instead of immediately
//  Default: "now"
Unattended-Upgrade::Automatic-Reboot-Time "02:30";
```

Here you can adjust the first setting to “false”, and/or change the reboot time to better suit your websites specific requirements.

To save the file hit CTRL+O followed by Enter, and then CTRL+X to exit nano.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

