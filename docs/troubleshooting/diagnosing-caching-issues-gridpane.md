# Diagnosing Caching Issues | GridPane

# Diagnosing Caching Issues

 

13 min read 

## Introduction

Caching issues can be a frustrating experience to go through, especially when it seems like all caching is completely turned off, or previously things were working just fine until right now.

Fortunately, these kinds of things don’t happen very often, and in this guide, we’ll cover some of the causes, including issues we’ve seen caused by some popular plugins/services.

### Table of Contents

###### Diagnosing Specific Caching Issues:

 

## Important: First Checks Before You Begin

If you have our caching disabled in your website’s customizer in your account (and you’ve synced the setting), and haven’t activated the GridPane Object Cache plugin, it simply isn’t possible that our stack is caching anything on your website other than PHP – which caches for 60 seconds.

We also completely exclude page caching for logged-in users when it is turned on – so if you’re logged in there is no page cache in play.

Also, if your website doesn’t look the way that it should, please ensure that you have the Nginx Helper plugin configured properly. You can check out this Redis Page Caching Guide and/or this FastCGI Page Caching Guide for full visual instructions.

### Incognito Mode

When checking for changes, it’s better to do so in incognito mode so that you rule out browser caching. Also note, that in incognito mode the browser will create a new temporary cache for the websites you visit during your session, and you will need to close ALL incognito windows for the cache to be deleted.

In other words, if rechecking, close all incognito windows and then try again by opening your website in a new incognito window.

### Hard-Refreshing

You should also “hard reload” when reloading/refreshing a page to check for changes. In Chrome, Edge, and Firefox, you can hard-refresh with CTRL+F5 on Windows.

In Chrome and Firefox on Mac, you can hard-refresh with Command+Shift+R. In Safari, you can use ⌘ Command + ⌥ Option + E.

### Disable Caching

Before you begin your diagnosis, you may wish to confirm the cache is fully clear by: –

 

## Here’s How to Confirm if GridPane Caching is Active

Once you have disable caching and cleared all your website caches as detailed above, here’s how to confirm if your website is being cached using Google Chrome.

First, open up your website in an incognito window. Next, right-click and choose “Inspect“, select the “Network” tab, and then reload the page. The result will look similar to the image below.

Click on your URL on the left-hand side to open up the box on the right, then down until you see the “Response Headers” section. If our caching is active, you’ll see the following for Redis Nginx Caching:

```
X-Grid-SRCache-Fetch
```

For FastCGI, you’ll see:

```
X-Grid-Cache
```

If neither of these are present, then our caching isn’t active. The website in the screenshot below has all caching turned off, and here you can see that the above options are missing from the response headers:

If caching is turned on, you’ll see either X-Grid-Cache or X-Grid-SRCache-Fetch with a value of either:

```
HIT | MISS | BYPASS
```

HIT means the website is cached.

MISS means this page hadn’t been cached yet as it’s the first time it’s been visited since either the cache has been activated or cleared -on reload, it should say HIT.

BYPASS means this page has been excluded and will never be cached.

Here is what Redis Nginx Page caching looks like when turned on (on activating, I got a value of MISS, but now the page has loaded, on reload, I have a value of HIT as shown below):

When logged into your website, you will see that the cache is bypassed, and in your dashboard, you will see:

```
cache-control: private, no-store
```

This forces browsers and CDNs never to cache.

Let’s get started.

 

## 1. Query Strings have been removed from CSS files

### The Problem

Updates to CSS aren’t being loaded on the website.

### Diagnosis

Open your website and right-click> Inspect as you did above. Look at the CSS files on the left-hand side. Do they look like:

```
style.min.css
```

Or like:

```
style.min.css?ver=5.12
```

The “?ver=5.12” version above is a query string. If you’re not seeing any query strings, then they have been stripped.

### The Underlying Cause

If query strings have been removed, something at either the website level or a CDN is stripping query strings from CSS files. It’s far more likely to be a plugin than anything else.

### The Solution

Now we need to find the cause. MainWP (more info below) is one plugin we know of that may do this. First, deactivate your CDN (this includes Cloudflare), and if that doesn’t fix the issue, begin deactivating your plugins one at a time until you find the culprit. As more information becomes available, we will update the list of plugins that are known to strip away query strings.

 

## 2. Multiple caches (layered caching) are breaking your website

### The Problem

Your website keeps looking broken and/or experiencing odd visual errors
### Diagnosis

Are there multiple caches at work on your website? Are you using our server caching as well as another caching plugin?
### The Underlying Cause

If you’re using both our server caching and a caching plugin, then these two aren’t going to be able to properly cache your website, and instead will be part caching your website, and part caching the other cache.
### The Solution

Choose either our server side caching or plugin caching (WP Rocket, Swift etc) and completely disable the other option. If you’re disabling the plugin, it’s a good idea to run the cache clear before doing so. Regardless of which option you stick with, run a full cache clear in the self help tools as illustrated above.								

## 3. Pages Look Broken After Updating or Making Changes

This specific issue is due to the way pagebuilders like Elementor, Beaver Builder, Divi, etc, implement and update stylesheets.

Elementor has also been a particularly bad offender for this when running updates as well.

### The Problem

On the front end of your website, when not logged in, some or all of your pages look like a broken mess, sometimes with lots of unstyled text.

### The Underlying Cause

Page caching will cache the stylesheet version that the page is using at the specific point in time the page is loaded into the cache.

On running updates or making changes to pages though, Elementor and other builders regenerate the stylesheet/s, and when this happens the previous version no longer exists.

After this, when you visit the page, the cache is trying to load this previous iteration which has since been replaced, and because it no longer exists, some or all of the CSS is now missing, and you end up with horrible, broken-looking pages.

If you check the console, you will see a 404 for the missing stylesheet.

### The Solution: Clear the Cache

On clearing the cache, the page loads the correct version, and this is then cached after the first load so everything works correctly again.

For individual pages, you can simply visit the page on the front end and hit the clear button in the admin bar.

After updating pagebuilders, you may always want to run a full cache purge.

 

## 4. Strange, buggy behavior and 504s after switching caching methods

If you’re experiencing 504s or other strange behavior in your site, and this is fixed by clearing the cache, then it’s likely that you have the wrong setting checked in the Nginx Helper plugin.

Make sure that the cache setting  (FastCGI or Redis page caching) inside Nginx Helper matches the setting you have in the UI.

 

## 5. Beaver Builder

There are a couple of different issues we sometimes see with Beaver Builder. Both of these are detailed below.

### Problem 1

Design edits made using Beaver Builder aren’t showing on the live site.

### The Underlying Cause

Beaver Builder has an automatic cache clear function which runs when you update a page, so it’s safe to rule this one out in most cases. The actual cause is usually either our server-side caching, plugin caching, your CDN’s caching, or your browser’s caching.

### The Solution

Clear the cache for your website, clear your CDN’s cache (if applicable), and view the page again in incognito mode.

### Problem 2

Design edits made using Beaver Builder aren’t showing, even when logged in and no matter what changes are made.

### The Underlying Cause

The cause for this is either a plugin that’s stripping query strings from your CSS or your CDN has cached the resource and is loading it from its cache instead of directly from your server.

### The Solution

Deactivate your CDN, and if that doesn’t fix the issue, begin deactivating your plugins one at a time until you find the culprit.

 

## 6. MIME type errors

A quick note: MIME type errors are usually linked to a pagebuilder.

### The Problem

Pages on your website look messy or broken

### Diagnosis

Right-click > Inspect to open up the developer tools and click the Console tab. Do you see a MIME Type error? If yes, click the URL of the asset. Does it lead to a 404 page? And is the URL a page builder asset?

If yes, then this issue has been correctly diagnosed, and what’s happening is that the asset is supposed to be a CSS file, but the browser is finding an HTML file (the 404 page) in its place. Seeing the file is the wrong MIME type, it throws this error.

### The Underlying Cause

The MIME type is a symptom, not the cause, but it is helpful for getting to the root of the problem. The reason your pages look broken is that the CSS files that are needed are not the ones the browser is trying to load, and this is because the pagebuilder cache is stale and serving old assets instead of your new ones.

### The Solution

Step 1: Clear your pagebuilder cache

Step 2: Clear any other type of caching you have enabled. Our server caching doesn’t cache any files that have query strings, but in this case, we may be caching the links to those files, and other caching plugins and CDNs may do so as well.

 

## 7. MainWP

### The Problem

Updates to CSS aren’t being loaded on the website.

### The Underlying Cause

MainWP has 2 security settings that strip out the query string from CSS files which means they are cached by the browser and any CDN you may be using. The browser, therefore, doesn’t load the new CSS changes.

### The Solution

In your MainWP account, open up the site you’re experiencing difficulties with and navigate to the “Security Scan” tab as shown below. Here you can disable the two Scripts and Stylesheet options to fix this issue.

Once done, please clear your website cache, CDN (including Cloudflare) cache, and open the website in incognito mode.

NOTE: MainWP isn’t the only plugin out there that may cause this stripping of query strings. Also, the old CSS files may still load if the website is being cached by a CDN. These resources normally aren’t cached when the query string is in place.

 

## 8. Cloudflare (and other CDNs)

### The Problem

The website isn’t showing content and/or design changes.

### The Underlying Cause

Your website is being cached by Cloudflare’s CDN services and is loading an older version (or older partial version) of the website instead.

### The Solution

Clear the cache inside your Cloudflare (or other CDN) account.

 

## 9. OPcache caching PHP for 60 seconds

### The Problem

When making changes to PHP files directly on your server, the changes aren’t immediately showing up.

### The Underlying Cause

When your server loads a PHP file, it’s compiled into opcode and stored in the server’s OPcache. On reloading the page to see your changes, you’re being served the cached version of your PHP file, instead of the newly updated one.

### The Solution

There are 2 courses of action you can take. You can:

Here’s our article that details how to do both of the above via CLI:

Configure PHP Version OPcache Settings

 

## 10. Theme edits / PHP / CSS / JS changes aren’t automatically purged from the cache

### The Problem

After making a change to a theme or plugin file (PHP, stylesheet, JS), the files aren’t being purged automatically from the cache by Nginx Helper.

### The Underlying Cause

If you are editing theme files directly, this is outside of the save_posts scope (the WordPress loop). This includes making any edits to CSS files, js files, functions.php, or any theme templates.

### The Solution

To set these changes live, you will need to run a full cache clear via either the Nginx Helper plugin or via the self-help tools inside your GridPane account.

 

## 11. Cache is being BYPASSed instead of HIT – sometimes seen with Woocommerce cookies

### The Problem

You have caching enabled, but when checking the response headers, you’re seeing that the cache is returning “BYPASS” instead of “HIT”.

### Diagnosis

GridPane will display the reason if the cache is being bypassed in the response headers. For Redis Page Caching, you want to look for:

x-grid-srcache-skip

For FastCGI it’s:

x-grid-cache-skip

This may be due to a variety of reasons, sometimes multiple reasons – and you first need to make sure you’re logged out of your website, as the cache is bypassed automatically for all logged-in users.

Cookies from adding an item to a shopping cart are a common cause for this. This may look like this:

x-grid-cache-skip: -http-cookie

Or it may be multiple reasons together:

x-grid-cache-skip: -query-string-http-cookie-request-uri

### The Solution

This will require your own investigation as it’s a website-level issue. The above is, however, something we’ve seen in Woocommerce stores.

Woocommerce will only set the session cookie for logged-in users, but we had reports of other extensions, such as Woo’s PayPal checkout gateway plugin, setting the cookie for logged-out users. This is one we looked into with a GridPane client, and they found that after landing on a page that hadn’t yet been cached, it would set the cookie on the next page. So, all cached pages were fine, but as soon as you landed on an uncached page, the cookie would be prematurely set.

The solution for this specific situation is cache priming so that all your pages are regularly cached and served to your visitors. You can learn about cache priming here:

Optimus Cache Prime – Cache Preloading

For other BYPASS issues, you may need to do some investigation, and sometimes plugins such as Asset CleanUp Pro can help with these kinds of issues.

 

## 12. CleanTalk

### The Problem

Forms on your website are giving an error/failing after a certain amount of time has passed.

### Diagnosis

This issue was recently reported to us, so this is what we learned based on our client’s feedback: If you check your browsers Developer Tools > Console, you’re likely going to see an admin-ajax error. Clearing the cache then fixes the error.

### The Solution

If you’re using CleanTalk, there’s a setting inside the plugin called “Use Static Keys for JS check“. The default setting for this is “Auto“. Our client solved this by changing the setting to “On“.

This should resolve your form issue – however, please keep a close eye on it to confirm.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

