# Keeping Your GridPane Account Secure | GridPane

# Keeping Your GridPane Account Secure

 

3 min read 

### Table of Contents

 

## Introduction

Your GridPane account allows you root-level access to all of your servers and instant administrator access to all of your WordPress websites. It is imperative that you keep your account secure to keep your business secure.

This article details the security measures we have in place as well as the steps we recommend that you as the account owner take to keep your account as secure as possible.

 

## Account Security Hygiene Recommendations

GridPane includes many default security measures out of the box, but it’s important that you employ your own security best practices. This applies to any and all accounts that you own, including Vultr, UpCloud, etc.

 

### Check if You’ve Been Pwned

You can check to see if your data has been leaked online at the following websites:

If your data has been exposed, you should update all of your passwords on the exposed accounts as soon as possible.

 

### Setup Two-Factor Authentication (2FA)

This article details how to set up 2FA for your GridPane account:

Using Two-Factor Authentication (2FA) with GridPane

 

### Team Member Security

If your account includes our team member feature, it’s important to ensure that your team members also employ appropriate security measures. This means strong passwords, 2FA, and good general security hygiene.

Your Admin team members have access to all your sites and servers, and Staff and Client team members could potentially cause serious damage to them as well.

 

## Default GridPane Security

In 2023, the most common attack vector responsible for 60% of hacked WordPress websites was stolen session cookies and compromised credentials. These attacks don’t just affect WordPress, though, but every website where you have an account.

We have built-in protections to protect your account, servers, and websites as much as possible should your GridPane account (or one of your team member accounts) is compromised.

The following account settings are secured by our one-time password (OTP) setting. If you haven’t set up 2FA, this is done via an email to your GridPane account email address.

 

### GridPane Features

The following server, website, and system user settings are secured by OTP:

 

### Account Settings Page

Your account settings page is secured by our OTP setting.

 

### API Integrations

Your API integrations and GridPane API key are masked, and your integration keys cannot be viewed after being set.

 

### Billing Information

Your billing information is located within your settings page and secured by OTP. Billing is only available to account holders, and team member accounts cannot view this information.

 

## OTP Timeout Settings

The OTP timeout settings that help keep your account secure default to a 15-minute timeout. This means that after entering your OTP, you will not be asked to re-enter it again for the next 15 minutes.

You can set a custom OTP session duration in minutes, with the maximum allowed duration being 120 minutes. This can be done inside your account Settings > Security page:

Logging out of your account will end the OTP session.

 

## Additional Reading

You may also be interested in the following articles:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

