# Why Can’t I Access My Server Stats (Monit) / PHPMyAdmin (PHPMA)? | GridPane

# Why Can’t I Access My Server Stats (Monit) / PHPMyAdmin (PHPMA)?

 

4 min read 

## Introduction

If you’re unable to open up your server stats (Monit) or PHPMyAdmin (PHPMA), in most cases it’s likely due to the browser that you’re using. Some browsers (including Safari and Microsoft Edge) will require you to go through HTTP authentication before it will opening up.

There may be other cases, however, that give you an SSL error, or simply timeout when trying to access the page.

Below we’ll look at each of these scenarios.

 

## 1. HTTP Authentication

If you’re using Chrome or Firefox you should be fine, but for the best experience we recommend using Google Chrome to access your GridPane account.

If you don’t want to switch over to Chrome, you can certainly still access this page, and to do so you just need to enter the HTTP authentication details.

The username is: gridpane

The password is the same for all of the sites on your server. To find it, head over to the Sites page and find a site hosted on this server. Next click on the log icon:

And you can find your password here:

 

## 2. SSL Errors

If you’re seeing an SSL error, there are two possible reasons. In either case, reach out to our support team with the server’s IP address if you’re not sure.

### Fixing Failed SSL Renewals

The SSL for Monit/PHPMA has failed to renew, and a new one needs to be manually provisioned. To renew the Monit SSL run the following command:

```
gp site monit -ssl-renewal
```

Copy and paste the following command to run your PHPMA SSL renewal:

```
gp site phpma -ssl-renewal
```

Next, check the crontab to make sure the cronjob for Monit’s SSL renewal was added. Use this command to view all the cronjobs:

```
crontab -l
```

The crontab should show something similar to this:

```
5 4 1 * * /usr/local/bin/gp site monit -ssl-renewal
```

If it is not there, add it in. Edit crontab with this command:

```
crontab -e
```

Choose nano as your editor. Add the line shown above. Write the file and exit (CTRL+O followed by Enter to save the file, then CTRL+X to exit nano).

This is also detailed in this knowledge base article:How to Manually Renew Monit and PHPMyAdmin SSL Certificates

 

## 3. Website is  Unsafe Warnings

If your SSL is all good, then here you’re antivirus software or ISP is probably blocking access.

One thing we’ve seen in support recently is an increase of reports where the client can’t access Monit (or PHPMyAdmin), but our support team can without any issues, and the SSL certificates are all valid.

In these cases, it has turned out to be some form of antivirus software (“Clean my Mac” in the most recent case), or the internet service provider flagging the links as dangerous.

One client ran into such an issue with Comcast Xfinity. They reported:

 

“Just a heads up, if you have Xfinity and you can’t access Monit or phpMyAdmin, then it’s likely they are seeing it as a “threat”.

To get around this problem, you have to go to https://internet.xfinity.com/connect then click on “Advanced Security”, then it should be obvious what to click on there until you get to “Threat History”.

On this page you’ll see a bunch of entries like:

“Content from xxxxxxxxxx.gridpanevps.com was blocked and is classified as: Phishing/Other Frauds.”

To the right of that is a button to “Allow Access” but it will only last for an hour.”

 

We’ve also seen this recently with BrightCloud, however they have since reclassified our domain as safe upon manual review per our request.

### Using a VPN

If you have a VPN you may be able to get around any ISP block and access Monit and/or PHPMyAdmin that way.

 

## 4. The Page is Timing Out

If you’re finding that the page is timing out then the server is either overloaded and can’t handle the request, or you may have been temporarily banned by Fail2Ban, which completely denies all access to the server for the duration of the ban.

If you’ve been banned by Fail2Ban, all websites on this server, as well as PHPMyAdmin will all experience the exact same error – the page looks like it’s trying to load but ultimately times out and fails.

You can learn more about unbanning yourself in Fail2Ban in this section of the Fail2Ban article:

Unbanning an IP Address in Fail2Ban.

The section before also details how to whitelist your IP address as well.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

