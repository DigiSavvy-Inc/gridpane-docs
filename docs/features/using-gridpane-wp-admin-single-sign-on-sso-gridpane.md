# Using GridPane WP-Admin Single Sign On (SSO) | GridPane

# Using GridPane WP-Admin Single Sign On (SSO)

 

5 min read 

GridPane has been set up to make managing your WordPress business as convenient and fast as possible.

We aim to provide the most powerful tool to enable you, to that end we have an integrated WP-Admin Single Sign On (SSO) feature that allows you to log directly in to your GridPane deployed WordPress sites with the single click of a button, no mess, no usernames and passwords to remember, just ruthless efficiency!

 

## Log directly into your WP-Admin

Locate the green WordPress logo next to your domain in the Active Sites list.

When you hover over it, a pop up caption will let you know this is the single sign on button.

Click the icon, and you will log directly in to your site’s WP-Admin…..

….once you have whitelisted the GridPane app with your browser pop up blocker.

 

## Popup Blockers and SSO

If this is the first time you have used GridPane WP-Admin SSO, then it is likely that your browser’s pop up blocker will block the login until you whitelist my.gridpane.com.

Different browsers have different processes, but they are usually very similar. In Chrome the process is as following.

Click on the icon notifying you of the pop-up being blocked, and a modal will appear detailing the single sign-on link that wants to open, and a choice to keep blocking or to allow pop-ups from my.gridpane.com.

<

Select the Always allow pop-ups and redirects from https://my.gridpane.com radio button, and click Done.

 

## Now Log Directly in

The modal will close, you need to reopen it, and this time click the link to log directly into your WP-Admin dashboard.

Alternatively, you could now just re-click the GridPane WP-Admin SSO button, and you will log in to your site directly.

 

## Two-Factor Authentication and SSO

We highly encourage the use of 2FA on your websites, but one of the potential downsides is that it will interfere with SSO. For example, recent testing with iThemes Security 2FA and the WP 2FA plugin still requires the 2FA code to be able to login successfully.

On the flipside, this can be great if you want the additional security on your websites.

 

## Enable/Disable GridPane WP-Admin Single Sign On

You might not want to always have Single Sign On enabled for your sites, so it is just as easy to disable it.

Open your site customizer by clicking on the site domain.

In the settings tab you will see a toggle for Single Sign On, the feature is enabled by default on all new sites deployed.

If you would like to disable SSO, then just flick the toggle to the off position.

The GridPane WP-Admin SSO button will turn red and become inactive.

You can re-enable SSO at any time by flicking the toggle back to the on position.

And the SSO button will turn green again, and become active.

 

## Troubleshooting

If you find that SSO isn’t working on one of your websites, this is usually due to a plugin on the site interfering.

### Step 1. Open the Logs Tab

However, that’s not always the case, and you should first being troubleshooting by checking the SSO log. You can view this directly from within your GridPane account by opening up your sites customizer and clicking through to the logs tab:

Now click the button highlighted above.

### Step 2. Checking your SSO log

This log keeps track of all SSO attempts and will let you know if WP-CLI was able to create a link successfully or not, and if not, why it was unable to do so.

#### If the link was created successfully but doesn’t work

If the link creation was successful, and SSO is working for you on other websites on the same server, then it is almost always a plugin that is responsible for the link failing to work.

If it has worked successfully, you will see the most recent attempts output look similar to this with the link it created:

```
**********************************************************************************************
sso Log Begin - example.com 
**********************************************************************************************
Sat Oct 10 11:24:40 UTC 2020
WPCLI Login Package is installed...
WPCLI Login MU plugin in place...
wpadmin_id.env exists - generating SSO link for admin ID 1
https://example.com/6455cc1a/6a86f9fc6e-d7d14cf61b-091895
Generating Payload:
Sending payload...
{"url":"example.com", "server_ip":"199.199.199.199", "status":"success", "login_link":"https://example.com/6455cc1a/6a86f9fc6e-d7d14cf61b-091895"}
```

#### If the server encountered an error when creating the link

Here you can see the exact issue.

For example, this is an example of an error caused by Composer needing a higher version of PHP:

```
Your Composer dependencies require a PHP version ">= 7.3.0". You are running 7.2.25-1+ubuntu18.04.1+deb.sury.org+1. Error Code: 100 | PHP Errors stopping SSO Link creation, please check logs….
```

To fix the specific above, please see this article:

Setting the CLI PHP Version

If you’re unsure of how to fix a different error that you’re seeing, please contact us on support with the output from your SSO log.

 

## Changing the Default SSO User

By default, our SSO feature uses the WordPress user with the lowest ID number inside the wp_users database table. It starts with WordPress user #1, and if that doesn’t exist, tries #2, and so on.

If you would like to change this to another user, it’s a quick simple process. This article has all the details:

How to Change the Default Single Sign On (SSO) WordPress Admin User

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

