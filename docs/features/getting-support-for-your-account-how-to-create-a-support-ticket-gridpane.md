# Getting Support for Your Account: How to Create a Support Ticket | GridPane

# Getting Support for Your Account: How to Create a Support Ticket

 

7 min read 

## Intro

In this article, we’ll take a look at the available options for opening a support ticket, how to track your ticket, and how to help us help you as quickly and efficiently as possible.

 

## Part 1. Support Options and Opening a Support Ticket

Support works a little differently for each account type.

### Panel Plan

Support for the Panel plan always starts in the Community Forum. Here you may well find a solution to your question already exists along with additional information that may also be helpful.

If it doesn’t then you can create a new post detailing your problem. If it’s an issue that only GridPane support can solve (for example, an issue with the GridPane application), then our team will create a support ticket for you inside our support desk and work with you there to resolve it.

### Support and the Community Forum

If you don’t already have an account on the Community Forum, you can create one here.

Generally, even for Developer accounts, the Community Forum is the best place to reach out for most issues as you’ll benefit from both our team’s input and the wider GridPane community as a whole.

Our team is constantly active in the forum, including team members who don’t actively work in support, so with this and the wider GridPane community, knowledge sharing (and preserving) is done in a way that EVERYONE can benefit from.

A tremendous amount of knowledge is lost forever inside our support desk. The community forum ensures that everyone can benefit from your questions and the answers you receive.

To get started with support, you can head straight to the Community Forum directly, or within your account, you can click on your name in the top right and choose “Community Support“.

### Opening a Ticket – Developer Plan & PeakFreq Servers

For Developer plan accounts and any accounts that have created PeakFreq servers*, you can open a support ticket directly by clicking on your name in the top right-hand corner inside your GridPane account, and then select “Create Ticket” from the dropdown:

Here you can choose the type of issue you’re experiencing and provide us with the details (more on this below), and also add any attachments that will help us in diagnosing and/or fixing your issue. Please always provide as much info as possible.

*Core and Panel plan tickets are limited to PeakFreq servers only.

 

## Part 2. Help Us Help You – Information We Need

For us to assist in the quickest, most efficient way possible, we need as much information as you can give us. There may be times that we won’t be able to do that much until we have more information about the problem you’re facing. Here are some guidelines to help us help you.

Some of the below are guidelines (especially the video captures in #2). Logs will be necessary depending on your issue.

 

### 1. Server IP and Website URL

If your support ticket relates to one of your servers and/or one of your websites, please let us know the IP address and provide us with a link to where the issue is occurring.

 

### 2. Screenshots and/or Video Captures (If it makes sense to do so)

A visual look at what you’re experiencing can save a lot of time if applicable. Screenshots for things such as error codes, or video captures

This of course depends on the nature and urgency of your issue. We certainly don’t expect videos for urgent site or server level issues, but it can be much easier to demonstrate a complex issue with a 2 minute Loom video vs trying to explain in writing what’s occurring and then have us interpret the issue and try to repeat the testing.

 

### 3. Server Errors – 50X, 40X etc

Please check your Nginx/OpenLiteSpeed Access and Error logs and attach them to your ticket as relevant. Please also provide us with the details necessary for our team to reproduce the issue on your website. The faster we can do this, the faster we can help you.

If you’re experiencing asset loading issues, please also provide console log output. You can do this by opening up the page of your website, right-clicking and selecting “Inspect” and then clicking on the Console tab:

 

### 4. HTTP 500 issues

Please provide us with the information in the Nginx Error log. These are almost certainly application level issues (an issue inside your websites codebase), so please also provide secure debug log output if possible.

You may also want to check out these troubleshooting articles to get a jump on the issue:

Diagnosing Performance Issues and 504 Timeouts

WP Debug and Query Monitor

 

### 5.1 SSL/HTTPS Issues

Please provide us with the SSL provision log output. The reason for the failure of your SSL is always detailed inside these logs.

Please also check your DNS resolution to make sure you’re DNS is resolving to your server (if you aren’t using a DNS API integration). This website is a great way to test your A and CName record propagation:

https://dnschecker.org/#A

Please also provide a screenshot and console log output (head to your website, right-click, choose “Inspect“, then select the Console tab and take a screenshot):

 

### 5.2 SSL Renewal Issues

If you’re getting notifications that your SSL has failed to renew, Let’s Encrypt will give you the exact reason for why it has failed to do so. You can find this directly in your renewal logs which are located here:

 

### 6. MySQL Issues

Please check your MySQL error log and provide the MySQL log output with your ticket.

You can find the Auth logs by heading to your Servers page inside your GridPane account, clicking on your server to open up the server configuration modal, and clicking through to the logs tab:

If it’s a database connection issue from WordPress, then please also activate WP Secure Debug and provide its log output:

 

### 7. SSH & SFTP issues

For SSH issues, please provide the error output from your connection attempts and the output from the Auth Logs when you attempt to connect.

For SFTP issues, please provide the error output from your SFTP client (a screenshot is fine) and the output from the Auth Logs when you attempt connections.

You can find the Auth logs by heading to your Servers page inside your GridPane account, clicking on your server to open up the server configuration modal, and clicking through to the logs tab:

 

### 8. Staging Push Issues

For any issues relating to staging pushes, please provide us with staging logs:

 

### 09. All other issues

We understand that not all issues fit nice and neatly into a specific category. If you’re not sure what’s going on, that’s OK. Please just try and give us as much information as possible so that we know where to begin with your ticket.

 

## Part 3. Tracking a Support Ticket

Once you create your first ticket in our support system will automatically create an account for you using the email attached to your GridPane account.

You can then view past and open tickets here: https://support.gridpane.com

In most cases, the system will send an account activation email with a link to get started.

If you have not received an activation email then your account has already been verified. In these cases, when you go to login for the first time, you will need to reset your password on the above page.

 

 

### Info

Due to incorrect information (site URLs, IP addresses etc) being submitted through the portal, and email address changes that mean our team cannot verify your account, ticket submission through the support portal has been disabled.

## Don’t Forget the Knowledge Base!

More often than not, the solution to the problem you’re facing is probably well documented here in our Knowledge Base. We also have a learning path for avoiding and troubleshooting the most common problems which we’d highly encourage you to check out here:

Learning Path: Solve and Avoid Common Problems

We do our best to keep our documentation up-to-date and continually add more to help you get the most out of our platform.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

