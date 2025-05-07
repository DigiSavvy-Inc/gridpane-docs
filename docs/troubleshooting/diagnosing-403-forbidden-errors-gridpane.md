# Diagnosing 403 Forbidden Errors | GridPane

# Diagnosing 403 Forbidden Errors

 

10 min read 

### Table of Contents

 

## Introduction: What is a 403 Forbidden Error?

The 403 Forbidden error occurs when a request is made the server cannot allow. This is often due to a firewall ruleset that strictly prohibits this specific request, but other settings such as permissions may prevent access based on user rights.

When 403s occur, your server understands the request that is being made, but is refusing to comply with the request.

That’s about all there is to it. Your request is forbidden.

### Error Messaging

On Nginx a 403 looks as follows: 403 Forbidden – nginx

Other variations of a 403 include:

 

 

### Note

The following are all certainly possibilities for your 403 errors, however, in 90% of cases, 403 errors are caused by a firewall, caching issue, or permissions issue.

### Connecting to Your Servers

Some of the following may require you to SSH into your server. Don’t worry, almost anything you may need to do via SSH by following articles here in our knowledge base is the equivalent of basic HTML difficulty-wise. Please see these guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## 1. Firewall Rules

By far the most common reason for 403 errors is that the request you’re making is being blocked for breaking one of the firewall rules.

Unlike most other hosting providers, GridPane equips you with 1-3 different Web Application Firewall (WAF) options depending on your plan: –

Usually, 403s are a good thing. In most cases, these types of requests are malicious in nature and the firewall blocks those from even reaching your application (WordPress website). However, WordPress is a vast ecosystem of different functionality and false positives can and do occur.

The quickest way to discover if your 403 error is being caused by a WAF is to simply turn it off and try to reproduce the issue. If the 403 no longer occurs, this is a WAF issue.

You can find out the specific reason the request is being blocked by checking the log. This is available directly inside the security tab at the bottom of the settings.

Once you know the cause, you can begin crafting an exclusion that is fairly straightforward, and fully documented in the links above.

### Example

Here’s an example of a request that resulted in a 403 error with the 7G WAF:

website.com/wp-admin/admin.php?page=seopress-google-analytics&code=4/0AY0eSoaWlA&scope=https://www.googleapis.com/auth/analytics.readonly

This request broke 2 rules, as detailed by this result in the 7G WAF log:

```
[17/Nov/2020:15:05:35 +0000] [":bad_querystring_12::bad_request_15:"] 199.199.199.199 yourdomain.com "GET /wp-admin/admin.php?page=seopress-google-analytics&code=4/0AY0e-g44ZrE9024kffJQ2LbRdRxVLOQgAruyU9wAHI1jYFCDaUo10xmwW5rpilPzqNKOSoaWlA&scope=https://www.googleapis.com/auth/analytics.readonly HTTP/1.1" 403 "https://accounts.google.com/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 11_0_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36"
```

Using this information we can create a rule to exclude these two results by targeting “page=seopress-google-analytics&code” and adding an exclusion for both errors like so:

```
set $exclusion_rule_match "";
if ( $args ~* ^page=seopress-google-analytics&code ) {
set $exclusion_rule_match 15;
}
if ($bad_request_7g = $exclusion_rule_match) {
set $7g_drop_bad_request 0;
}
```

```
set $exclusion_rule_match "";
if ( $args ~* ^page=seopress-google-analytics&code ) {
set $exclusion_rule_match 12;
}
if ($bad_querystring_7g = $exclusion_rule_match) {
set $7g_drop_bad_query_string 0;
}
```

Please see the full articles for a complete tutorial.

 

## 403 on an Image or File

Following on from the above section, images or files may sometimes return a 403 for a seemingly unknown reason.

These can be difficult to troubleshoot because it’s really not obvious what the cause is, however, this is almost certainly

A couple of examples to illustrate this are images/files that contain either the word “Specialist” or the word “Conference”.

The reason these get flagged are due to the word conference containing “conf” (which is a file name extension), and specialist containing the name of a commonly spammed pharmaceutical.

The quickest solution is to rename the file, or to edit out that specific line or word in the firewall. Our documentation has details how to do this here:

Using the GridPane 7G Web Application Firewall

 

## 2. Caching and Nonces

The second most common issue outside of a firewall rule being is broken is where caching is interfering with a form (such as a contact form, or payment gateway form). Here, the form uses what’s called a “nonce” (a security token which is a number or random string used only once), which exists for a set period of time (12 hours is common) after which it changes to something new. Once change occurs, the cache may serve the outdated nonce and this results in an error.

If you have a form or any functionality that makes use of a nonce, these can break and return 403 errors if the cache isn’t cleared once the nonce expires.

In many cases, nonces last 12-24 hours. For example, the Gravity forms payment gateway has a 12-hour nonce and can result in 403 errors if cached for over 12 hours.

If clearing the cache allows your functionality to begin operating correctly again, this is a caching issue.

Plugins we know of that may experience cache related issues are:

In these cases, there are a couple of different solutions.

### Solution 1. Exclude the page from the cache

If you exclude the page from the cache, the cache will not interfere with the nonce and all forms will operate as normal.

Please see the following guide on how to exclude a page from your website’s cache (Nginx only):

Exclude a page from server caching

### Solution 2. Reduce Cache TTL

If you’re using Redis Page Caching, the default TTL is 30 days. If you’re experiencing nonce related form failures, you can reduce the cache time to avoid these in the future.

This requires running a single GP-CLI command. To do so, you will need to SSH into your server. Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

The command for altering the default caching TTL is as follows:

```
gp stack nginx redis -site-cache-valid {accepted.value} {site.url}
```

Run the following command to reduce cache time to 6 hours (replacing site.url with your domain name):

```
gp stack nginx redis -site-cache-valid 21600 site.url
```

The time length has to be entered in seconds. In this case, 6 hours = 21600 seconds.

For 10 hours, run the following:

```
gp stack nginx redis -site-cache-valid 36000 site.url
```

For more details, please see this Redis Page caching section in the Configure Nginx article:

Set caching expiry time for all successful requests going into Redis SRCache page cache

 

## 3. Permissions

403 errors can also be caused by incorrect permissions settings. This can sometimes occur when migrating a website over to GridPane.

Fortunately, we have a quick fix self-help tool that can help reset your website to the correct permissions very quickly and with minimal fuss. To fix your websites permissions, please see this article:

Self Help Tools: Reset Application File Permissions

 

## 4. CDN Issues

If the 403 forbidden errors you’re experiencing are specific to your assets (images, CSS, and JS files), and you’re using a delivery network (CDN) for your website, try temporarily disabling this service to see if this is at the root of your issue.

If it isn’t, this is likely firewall related, possibly due to 7G Bad Bot rule #5.

 

## 5. Corrupt/Misconfigured .htaccess File

Nginx doesn’t use .htaccess, so this error is OpenLiteSpeed specific for GridPane hosted websites.

This is a very powerful file, and if corrupted or misconfigured, this could result in a 403 error for your website.

Fortunately, GridPane keeps a backup copy that you can use in the case of an emergency:

You can get your website back up and running by replacing the current .htaccess file with the contents of the .htaccess.save file.

This is easier done over SFTP. To connect to your server over SFTP, please see either one of the following articles:

Connect to a GridPane Server by SFTP as System User

Connect to a GridPane Server by SFTP as Root user

##### Step 1

Once connected, first save a copy of the .htaccess.save file to your computer.

##### Step 2

Next, rename the corrupt .htaccess file to .htaccess.bad

##### Step 3

Next, rename .htaccess.save to .htaccess and then check your website.

##### Step 4

You can now re-upload the .htaccess.save to your server again for safekeeping, and delete the .htaccess.bad file.

 

## 6. Missing WordPress Core Files

If there are missing Core WordPress files on your site, or if one has been moved to another directory for some reason (I can recall one case where a client had decided to move their wp-settings.php file outside of htdocs, then created an emergency support ticket without any details of what they’d just done). We’ve also seen a missing index.php cause 403 errors.

This may result in either a 403 or a 500 error. The previous section above contains a list of the files inside htdocs – note that those that begin with a “.” are hidden files.

You can run a check with the following command (replace site.url with your domain name):

```
gp wp site.url core verify-checksums
```

For example:

```
gp wp yourwebsite.com core verify-checksums
```

This will check your core WordPress installation files and let you know if any issues need to be addressed.

This type of issue is usually the result of malware.

 

## 7. Broken/Missing Theme or Plugin Files

If none of the above is the cause for your 403 error, then this could be the work of a broken or missing plugin file.

To check, connect to your server over SFTP (see the links in part 5 above to get started) and rename the plugins folder (located at site.url/htdocs/wp-content/plugins) to plugins-off.

Next, check your website and see if the 403 error is occurring. If not, then you know the root cause is one of the plugins on your website.

Rename the plugins-off directory back to plugins, and then do the same for each of your individual plugin folders, renaming them one by one until you find the one responsible.

 

## 8. Custom Nginx Configurations

Sometimes plugin authors can be rather careless with their Nginx recommendations, documenting broad Nginx rules that can result in unexpected/undesirable behavior such as blocking specific types of files altogether, or blocking them when not logged into the website.

You may have added custom configuration rules to Nginx via .conf files in your  /var/www/site.url/nginx directory.

For example:

```
/var/www/example.com/nginx/ithemes-security-main-context.conf
```

Custom configurations that affect ALL websites on the server may also have been added in these directories:

```
/etc/nginx/extra.d/
```

```
/etc/nginx/conf.d/
```

Be sure to check this directory for any Nginx configuration files that you or your team members may have added (be sure to ask them so you know what to look for), and review them for code that could prevent access to page or file that your getting your 403 forbidden error.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

