# Troubleshooting the SendGrid SMTP Integration | GridPane

# Troubleshooting the SendGrid SMTP Integration

 

4 min read 

## Introduction

Previously, our SendGrid integration worked right out of the box once toggled on for the site you wish to use it on. More often than not now though, you will likely need to verify your domain with SendGrid for them to start sending mail from your website.

### Table of Contents

 

 

### Information

All emails are autoconfigured to be sent from [email protected]. This applies to subdomains, so on staging, etc, it will be [email protected].

In the future, this feature will allow for the from sender to be user-defined.

## About Our Integration

Our SendGrid integration is fairly simple – we drop in a plugin that contains your API key and then pass it along to SendGrid.

That’s all there is to it, so as long as you don’t have a competing mail system that could potentially interfere, it provides and quick and easy solution to get your website mail up and running.

Below are instructions for troubleshooting ALL of the issues we sometimes see when getting SMTP up and running.

### Additional Note

Also, when mail is failing to send due to the domain not being authenticated or the API being incorrect, WordPress should return the “Error: The email could not be sent. Your site may not be correctly configured to send emails. Get support for resetting your password.“. However, this should not be relied upon as an indicator.

 

## 1. Domain Authentication

First, try authenticating the domains you’re trying to send mail from. This is always a good idea anyway to ensure ongoing delivery, but as of April 2020, we’ve had multiple reports of this immediately fixing emails not sending. SendGrid and all SMTP providers are clamping down on sending emails from unauthenticated domains.

Here is SendGrid’s knowledgebase article on how to do this: –https://sendgrid.com/docs/ui/account-and-settings/how-to-set-up-domain-authentication/

 

## 2. Test Your API Key

Below is a simple copy and paste code block you can use to test your SendGrid API key and the domain you’re having issues with:

```
curl -i --request POST \--url https://api.sendgrid.com/v3/mail/send \--header 'Authorization: Bearer {api-key-here}' \--header 'Content-Type: application/json' \--data '{"personalizations": [{"to": [{"email": "[[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)"}]}],"from": {"email": "do_not_reply@{domain.com}"},"subject": "SendGrid Test!","content": [{"type": "text/plain", "value": "Howdy!"}]}'
```

Switch out the parts highlight above with your API key, your email address, and the domain you’re trying to send mail from.

Next, simply copy and paste it into any one of your servers. You will be given the exact reason for the failure. For example:

```
{"errors":[{"message":"The from address does not match a verified Sender Identity. Mail cannot be sent until this error is resolved. Visit https://sendgrid.com/docs/for-developers/sending-email/sender-identity/ to see the Sender Identity requirements","field":"from","help":null}]}
```

Now you’ll know whether it’s an issue with your API key. If it isn’t and the mail sends successfully, then follow the steps below.

 

## 3. Additional Troubleshooting Steps

If you’ve found your emails aren’t sending, below are the next steps and possible causes.

### 1. Emails are Landing in Junk/Spam or Being Outright Rejected

Are emails being sent to spam or missing your inbox entirely? Check your SendGrid logs within your SendGrid account. Are the emails showing up? If they are, then your emails may be going to your spam folder, or possibly not even making it that far. For this, you will likely need to authenticate your domain so that email services know that SendGrid is fully authorised to send emails on your behalf.

### 2. Your Provider is Blocking Outgoing Mail

Linode users: Linode restricts access to ports that are used for mail delivery via SMTP. Follow this article to get them unblocked for your server.

The other providers we integrate with via API typically don’t do this. Any custom server provider might do.

### 3. Enable WP_DEDUG

Enabling WP_DEBUG will log any error output from either wp_mail error or from php_mailer -> SMTP. You can learn more about using WP_DEBUG here.

### 4. Check for an SMTP Plugin Conflict

Are there any other mailer-type plugins installed? Another SMTP plugin may be interfering with our integration. If there is, please deactivate it and try again to see if this fixes the issue.

### 5. Regular Plugin/Theme Conflict

First, deactivate all plugins and retest sending email. If it works, you’ve confirmed that there is a conflict with a plugin in your website.

You can also do the same with the theme, but this far less likely to be the cause.

### 6. Your API key isn’t working correctly

Note: Ignore this step if the integration is already working on your other websites.

Try regenerating a new API key and make sure it has full access. Once done, add the new key to GridPane and toggle the integration off and back on again for your website.

### 7. You’ve Updated Your SendGrid API Key

If you’ve already updated your API key, be sure to toggle the integration off and then on again to ensure your new credentials are added to your website.

 

## Wrapping Up

Hopefully, at this point, your mail is now working correctly, but if none of the above gets you going, the next step would be to reach out SendGrid’s support to find out what’s going on from their end.

https://sendgrid.com/docs/ui/account-and-settings/support/

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

