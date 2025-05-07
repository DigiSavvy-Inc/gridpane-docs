# How to Manually Renew Monit and PHPMyAdmin SSL Certificates | GridPane

# How to Manually Renew Monit and PHPMyAdmin SSL Certificates

 

2 min read 

On occasion, some Monit and PHPMyAdmin (PHPMA) SSL certificates fail to automatically renew, which can result in these becoming unavailable due to an SSL certificate error (for example “NET::ERR_CERT_INVALID”).

It’s important to note that this is only one of the possible reasons why this may not be able to access Monit/PHPMA, and you may also want to check out this article if you find that both are inaccessible at the same time:

Why can’t I access server stats / Monit?

Renewing SSL certificates is something our support team can assist with, however, if you’d simply like to take care of this yourself immediately, below details the two GP-CLI commands for running the SSL renewals.

## Getting Started

To run the commands detailed below, you will first need to connect to your server over SSH. If this is your first time accessing your server over the command line, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

 

### IMPORTANT

Though the following will fix 99% of cases, if you find that the commands below don't complete successfully, please do not run them a second time. Instead, reach out to our support team with your server IP and the output from running the command. We can then diagnose where things may be going wrong.

## Renewing Monit SSL Certificates

Copy and paste the following command to run your Monit SSL renewal:

```
gp site monit -ssl-renewal
```

 

## Renewing PHPMyAdmin SSL Certificates

Copy and paste the following command to run your PHPMA SSL renewal:

```
gp site phpma -ssl-renewal
```

 

## Keeping Track

Like all SSL certificates, Monit and PHPMA will attempt to renew every month and you will receive notifications inside your account about failures 30 days in advance before they expire.

When any SSL renewal attempts fail, you will find the specific site and the reason for the failure inside your server’s SSL monitoring logs.

You can view your server logs by heading to the Servers page inside your GridPane account, and clicking on the name of your server.

This will open up the server customizer modal as shown in the image below, and the logs are contained in the Logs tab. To open up a log, simply click on the icon next to the log name in the view column.

The notification will tell whether you need to check the Acme Monitoring Log or Certbot Monitoring Log.

Monit and PHPMA will always be logged in the Certbot Monitoring Log.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

