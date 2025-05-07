# Diagnosing 520 Errors | GridPane

# Diagnosing 520 Errors

 

6 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

## Introduction

520 errors are CDN-specific, not web server-specific, and are a catch-all error. With Cloudflare, the most common service where we see 520 errors, this means that the web server returned an unknown error. This “I’ve no idea what’s going on” error makes it a bit of a nightmare to troubleshoot.

The bulk of this article will primarily focus on Cloudflare, but the same troubleshooting steps will likely hold true for most CDNs who are also adopting the same error codes.

That said, you may still want to Google “520 Provider Name” (for example, “520 QUIC.cloud”) though, as that may provide some more relevant troubleshooting steps.

 

## Cloudflare’s Breakdown

Cloudflare has its own documentation for troubleshooting 5XX errors. This can be viewed here:

Troubleshooting Cloudflare 5XX errors

In the above article, they state that this can be caused by:

### What We’ve Seen

Typically 520 errors are pretty rare when using Cloudflare with GridPane, and the second option can be ruled out unless you yourself have reconfigured that.

An empty response or excessively large headers (typically a lot of cookies) are the most likely culprits. Cloudflare may also have closed the connection early.

Too many cookies seem to be one of the most common issues, and the Cleantalk plugin [again] was the culprit of a recent case combined with Chrome storing these cookies for an excessive period of time. Full details can be found here in the community forum:

https://community.gridpane.com/t/cloudflare-520-errors-backend-unusable/1269/22

 

## Troubleshooting Steps

Usually, the best option when you encounter a 520 error is to disable Cloudflare’s proxy or your CDN, but in the unlikely event that there’s an issue with

### Step 1. Check Your DNS Records are Correct

It’s possible that you may be having DNS issues. Check that your DNS records are pointing to the right place.

### Step 2. Check Your Site in an Incognito Window

If your site is serving a lot of cookies and your browser has cached a lot of cookies, the issue may be local to you. Check your site in incognito (even in a new browser) to see if the issue still occurs.

### Step 3. Check the Cloudflare (or your CDN) Status Page

Maybe Cloudflare or your CDN is having an active incident that’s causing issues in pockets around the world. Check Cloudflare’s status page for issues here:

https://www.cloudflarestatus.com/

If issues are reported, deactivate the proxy.

If you absolutely do not want to disable Cloudflare, you can create a HAR file. See the section below.

### Step 4. Check Monit

To open Monit, head to your Servers page inside your GridPane account and click the green pie chart icon next to your server:

### Step 5. Deactivate Cloudflare

Ruling out Cloudflare of the cause is usually the best option. From there, if there are no further issues, you know it’s Cloudflare (or other CDN) and not your server.

If issues continue to happen, then you will get the correct server error and can troubleshoot accordingly.

Once you’ve identified and resolved the underlying issue you can turn it back on.

### Step 6. Check Your Logs

With Cloudflare out of the way, any server errors will now provide insight on how to proceed.

The website error logs may also provide some legitimate website errors that could potentially be causing issues.

Check your website’s Nginx or OpenLiteSpeed error log. You can find this inside your GridPane account by heading to your Sites page and clicking on the name of the site to open up the customizer. Click through to the logs tab and you will find the error log at the bottom:

When checking the log, look for the errors that correspond to your website checks.

You can also activate WP Debug by clicking the toggle at the top of this tab, and this will install the query monitor plugin and potentially log more specific errors. More details on this can be found here:

WordPress Debug and Query Monitor

 

## Create a HAR File

A HAR is an HTTP archive file, and if you’re contacting Cloudflare support you will need to provide them with one (and it’s also a good idea to do the same for other CDN providers as well).

A HAR file will record all requests made by the browser, including the request & response headers (so you can confirm if your site’s headers are too large for Cloudflare). HAR files are also useful when troubleshooting issues that are difficult to replicate.

### 1. Create a HAR file in Chrome

1. Head over to the URL where you’re experiencing 520 errors, right-click and choose Inspect:

2. Next, click through to the Network tab. The circle in the top-left should already be red, but if it’s grey, click it. Also check the “Preserve Log” checkbox.

3. Now refresh the page. Here we want to record the page load with the error occurring.

4. Once you’ve captured that, right-click on any of the filenames in the bottom left, and choose “Save all as HAR with content“.

You’ve created your HAR file.

### 2. Create a HAR file in Microsoft Edge

The process for Edge is the same as Google Chrome. The screenshots in the above section are from Chrome, but you can follow them step for step in Edge too.

### 3. Create a HAR file in Firefox

The process is almost the same as Chrome:

### 4. Create a HAR file in Safari

 

## If 520 Errors Continue

If you’ve followed the above steps and you still see issues when you turn Cloudflare or your CDN back on, contact their support.

### Contacting Cloudflare

When reaching out to Cloudflare support they will ask for the following:

https://support.cloudflare.com/

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

