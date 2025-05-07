# How to Change Your Servers Time Zone and Automatic Security Reboot Time | GridPane

# How to Change Your Servers Time Zone and Automatic Security Reboot Time

 

3 min read 

## Introduction

If you’d like to change the time zone and/or the time that our automatic security updates take place for your servers, this can be done quickly and easily directly inside your GridPane account dashboard.

Below we’ll take a look at how to adjust your default time zone and security reboot time that will be applied for newly provisioned servers, and then how to configure servers individually.

 

 

### Security Updates Automatic Reboot

We push all new security updates within 24 hours of them being released. If a reboot is needed for these updates to take effect, Unattended Upgrades schedules this for the following 02.30 UTC time slot (unless you specify otherwise). The process is automatic by default, and the reboot only takes about 30-60 seconds on average.

## Default Time Zone and Security Update Settings

Out of the box, the default time zone for all servers is UTC, and 2.30AM for security reboots. You can easily set a different time zone and restart time if you would prefer to do so.

### Step 1. Navigate to settings > Default server build settings

Inside your account, head over to your settings page and click through to the “Default Server Build Settings” located on the left-hand side as pictured below:

### Step 2. Adjust your settings

Here you can adjust your default settings to whichever time zone makes the most sense for your business.

You can also adjust the time when automatic security updates take place for those updates that require a server reboot.

### Reset to default

If you’d like to reset to our standard default settings, simply click the big “Reset to GridPane Default” button.

 

 

### Info

Here you can also choose to disable automatic updates. We highly recommend that you leave them turned on, especially as the default. The downtime from such reboots are minimal, and this ensures that your servers are kept up to date with the latest security patches.

## Server Specific Settings

The defaults you set above will be automatically applied to all new servers that you create. If you’d like to adjust those settings for an individual server (for example, if you have servers on the other side of the world), this is quick and easy.

### Step. 1 Open the server customizer

Head to your GridPane dashboard and click through to the Servers page andclick on the server you wish to adjust:

### Step 2. Adjust your settings

First, hit the “Sync Settings” button if needed – if the settings appeared greyed out as below this will then allow you to change them once synced up:

Now you can adjust your settings to so that they make sense for your server’s location.

Once you’ve made your choice simply hit the Update button and you’re all set!

That’s it, all done.

 

## Legacy

Below is how to set your default time directly on the command line. We recommend that you do this via your dashboard for simplicity, but if you’d prefer to it directly or simply want to know how it’s done, below will walk you through the process.

### Default Server Time

As mentioned above, by default your servers will be on UTC time. You can confirm this by typing the following command and pressing enter:

```
date
```

The output will look like this but with the correct date and time: Sat Jul 25 17:18:12 UTC 2020

### Update your Timezone via the Command

First run the following to list available timezones:

```
timedatectl list-timezones
```

Use your down-arrow key to navigate down until you find your timezone, and hit Control+C to exit once you’ve got it.

You can now reset your timezone with this command:

```
sudo timedatectl set-timezone
```

Examples:

```
sudo timedatectl set-timezone Europe/Paris
```

```
sudo timedatectl set-timezone Asia/Singapore
```

```
sudo timedatectl set-timezone America/New_York
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

