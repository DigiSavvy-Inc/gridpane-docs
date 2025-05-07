# Server Updates / Maintenance / Security Patches - What Updates Does GridPane Take Care Of? | GridPane

# Server Updates / Maintenance / Security Patches – What Updates Does GridPane Take Care Of?

 

2 min read 

## Introduction

We often get asked whether anything is necessary on your part to keep your servers up-to-date and secure. In a nutshell, you are not required to maintain your servers, and this is included as a part of our service while they are still attached to your GridPane account.

### Table of Contents

 

## What Exactly Does GridPane Take Care Of?

GridPane takes care of all necessary server updates. This includes all security-related updates. For package updates that aren’t security related, these are updated if there’s a benefit in doing so. Many packages that come included as a part of the default OS install are simply not necessary for the operation or security of your servers and can be safely ignored.

Nothing is required on your part to maintain our default stack or your servers OS. As long as your server is up and running at your IaaS provider, then we will ensure that the server stack is enterprise-ready. More details below.

 

### Unattended upgrades

Unattended upgrades runs security updates for all system applications. It runs checks twice daily for security updates and is set to install and auto reboot if required at a time you can control. See below.

 

### Server Restarts

Servers often get restarted at 2.30am UTC to take care of these updates. If this time isn’t convenient for you, you can change your server’s time zone to one that makes sense for your business, and you can also adjust the time where these updates take place.

To update your time zone and/or default security reboot time, please check out this KB article:

How to Change Your Servers Time Zone and Automatic Security Reboot Time

 

## Exceptions: Software That You Install

For anything external that is installed by yourself and not us here at GridPane, this isn’t something that we would automatically update and is beyond the scope of our support. In these cases, maintenance of this software would be up to you to keep an eye on and take care of.

You can learn more about using third-party software in this KB article:

Can I Install Third-Party Software and Services on my GridPane Servers?

 

## What About OS Upgrades?

When it comes to OS upgrades, for example, Ubuntu 18.04 to 20.04, this is a nontrivial process.

There’s really no feasible way for us to support this. It’s not the straightforward process that it appears to be on the surface, and it can’t simply be automated. Hiring a sysadmin to manually upgrade the OS of a live production server would be no small investment.

Moving from 18.04 to 20.04 will require a newly provisioned 20.04 server and migrating your sites across. While there is some time involved, this is easy to do using the full server clone option, which will copy all your sites and their settings across.

Cloning One Entire Server to Another

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

