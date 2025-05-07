# How to Reduce Eric Jones Spam (and all the other Contact Form Spam) | GridPane

# How to Reduce Eric Jones Spam (and all the other Contact Form Spam)

 

12 min read 

## Introduction

I think we can all agree that whoever Eric Jones is, he’s a huge PIA. And a genius, but mostly a PIA.

Recently, one of my sites started getting relentlessly hammered with “Hey, my name’s Eric and for just a second, imagine this…“, as well as a bunch of other junk that landed straight in my spam folder. It’s a nuisance, and spam is always a constant battle, so I figured I’d set out to solve this (at least until these spammers implement a workaround).

### Table of Contents

You may also be interested in this article on preventing comment form spam:How to Stop WordPress Comment Spam Permanently (for FREE)

 

## Diagnosis: What Does ALL this Spam have in Common?

My contact forms collect the IP address and user agent of the sender. Unfortunately, the user agent is never simply a bot that we can easily target and block. In my case it was: Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0. Throwing that into Google does provide some info, and while it’s extremely unlikely the blocking this could block legitimate visitors, there’s no guarantee it will be the same user agent next time around. This is something I’ll be monitoring in the coming weeks in a test site.

Blocking the IP would essentially be useless as well because this will be different the next time. The IP is useful for gathering some extra information though.

Two things that are very likely to be true though are:

### Checking the Website Access Logs

I grepped 30 days of access logs and the IP from this particular message was only recorded in one “visit”. Here’s an example command for GridPane Nginx servers:

```
zgrep "199.199.199.19" /var/log/nginx/mywebsite.com.access.log*
```

And here’s an example command for GridPane OpenLiteSpeed servers:

```
zgrep "199.199.199.19" /var/log/ols/mywebsite.com.access.log*
```

Below we can see the sequence of events leading to the form submission:

```
[10/Feb/2022:15:42:24 +0000] 199.199.199.19 - - mywebsite.com "GET / HTTP/1.1" 200 8830 0.000 "-" "Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0"
[10/Feb/2022:15:42:25 +0000] 199.199.199.19 - - mywebsite.com "GET /contact/ HTTP/1.1" 200 8358 0.001 "https://mywebsite.com/" "Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0"
[10/Feb/2022:15:42:26 +0000] 199.199.199.19 - - mywebsite.com "GET /about HTTP/1.1" 301 0 0.000 "https://mywebsite.com/" "Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0"
[10/Feb/2022:15:42:27 +0000] 199.199.199.19 - - mywebsite.com "GET /about/ HTTP/1.1" 200 12906 0.000 "https://mywebsite.com/web-design" "Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0"
[10/Feb/2022:15:42:28 +0000] 199.199.199.19 - - mywebsite.com "GET /contact HTTP/1.1" 301 0 0.001 "https://mywebsite.com/" "Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0"
[10/Feb/2022:15:42:29 +0000] 199.199.199.19 - - mywebsite.com "GET /contact/ HTTP/1.1" 200 8358 0.000 "https://mywebsite.com/contact" "Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0"
[10/Feb/2022:15:42:32 +0000] 199.199.199.19 1.620 - mywebsite.com "POST /wp-admin/admin-ajax.php HTTP/1.1" 200 98 1.624 "https://mywebsite.com/contact/" "Mozilla/5.0 (Windows NT 6.0; Win64; x64; rv:50.0) Gecko/20100101 Firefox/50.0"
```

9 seconds total from start to spam. Pretty impressive.

We can confirm here that these requests were all made over HTTP/1.1. No legitimate website traffic will be using anything less than HTTP/2.0 (the GridPane stack and modern browsers automatically assure this), so now we have something concrete to work with.

Checking further, there were a total of 7 instances in Jan 2022 where this user agent sent a message via HTTP/2.0. Any solution addressing this therefore isn’t perfect, but it was a drop in the bucket of total submissions and it will still block a massive amount of spam.

Also, the series of events above is the only time the IP was used to spam me. It wasn’t used to send multiple form submissions.

 

## Solution 1: Block HTTP/1.1 Requests On Contact Pages

The spammers are using a “legitimate” user-agent (sort of) and regularly changing their IP, BUT they’re also using an outdated HTTP version that no legitimate visitors use. We can create rules that will block this traffic from being able to access our contact pages or /wp-admin/admin-ajax.php (though blocking admin-ajax.php could have unintended consequences and I wouldn’t recommend it).

### Whitelisting Good Bots

One thing to keep in mind here is that we don’t want to block the search engine bots (and potentially any other bots that you do want crawling your site). So we want to block HTTP/1.1 with the exception of specific user agents like Googlebot (even though this now uses HTTP/2.0 I’d rather have the exception in place just in case).

I’ll be whitelisting the following:

*When testing this, it was on a site where I’d also tested Cloudflare’s load balancing feature, and Cloudflare was getting blocked and sending me messages that my site was down.

You may want to whitelist a few other bots. KeyCDN has a rundown of other search engine bots here:

Web Crawlers and User Agents – Top 10 Most Popular

 

## Solution 2. Block admin-ajax.php Access Where the Referer Isn’t Your URL

A second way to tackle this is to block submissions that aren’t made directly from your website. This will allow your website to function normally, but direct access to the admin-ajax.php file is denied, and so bots won’t be able to post spam in the usual automated fashion. Both of these can be used in conjunction with one another, but either should be enough to solve your spam problems.

 

## Block with Cloudflare Option 1: Block HTTP/1.0/1.1/1.2 Method

This is the easiest option to implement. Cloudflare’s free firewall rules offer a quick and simple way to accomplish this.

In my case, I’m going to just go ahead and block everything prior to HTTP/2.0 unless it’s a user-agent I’m whitelisting. You can configure this how you wish.

 

 

### Important

The Cloudflare proxy must be active on your website for the firewall rules you set to take place. Please ensure that you set orange clouds for your A and CNAME records.

### Step 1. Create a Cloudflare Firewall Rule

Inside your Cloudflare account choose your website and then click through to the Security > WAF page. Here click the Create a Firewall Rule button.

### 2. Configure Your Firewall Rule Expressions

First, give your rule an easy to identify name.

Here is what my rule looks like:

This states that if:

If you’d like to use the same, or use this as a starting point, you can copy the following expression:

```
(http.request.version in {"HTTP/1.0" "HTTP/1.1" "HTTP/1.2"} and http.request.uri eq "/contact/" and not http.user_agent contains "Googlebot" and not http.user_agent contains "Bingbot" and not http.user_agent contains "DuckDuckBot" and not http.user_agent contains "facebot" and not http.user_agent contains "Slurp" and not http.user_agent contains "Alexa")
```

Next, inside your Firewall rule, click “Edit Expression” and paste the above.

From here you can continue editing the firewall rule to your liking.

### 3. Set the Action

I chose to outright block this traffic, but one of the great things about Cloudflare is that you can use their managed challenge or JS challenge to screen this traffic instead. Choose the option that you feel best suits your needs.

### 4. Deploy Your Rule

When ready, click the Deploy button to set your new firewall rule live.

Also, ensure that you have orange clouds active on your A and CNAME records so that traffic to your site is passing through Cloudflare’s system.

Cloudflare will now block Eric Jones spam, all other types of junk.

 

## Block with Cloudflare Option 2: Referer Method

The following can be used as an alternative to the above two rules. It blocks submissions that aren’t made directly from your website.

 

 

### Bonus!

You can also use this to prevent comment spam. Details included below.

### Step 1. Create a Cloudflare Firewall Rule

Navigate to the Security > WAF page, and click the Create Firewall Rule button.

### Step 2. Configure Your Firewall Rule Expression

First, give your rule an easy to identify name.

Here’s what the rule looks like:

This states that if:

If you’d like to use the same, you can copy the following expression (be sure to replace the URL with your own website):```
(http.request.uri contains "/wp-admin/admin-ajax.php" and http.request.method eq "POST" and not http.referer contains "yourwebsitehere.com") or (http.request.uri contains "/wp-comments-post.php" and http.request.method eq "POST" and not http.referer contains "yourwebsitehere.com")
```

Next, inside your Firewall rule, click “Edit Expression” and paste the above.

### Step 3. Set the Action and Deploy Your Rule

Cloudflare can block all requests that break the rule outright. When ready, click the Deploy button.

 

## Block with a Server Config

Both Nginx and OpenLiteSpeed have includes that make it easy to add additional rules to your websites (and server-wide rules on Nginx).

### GETTING STARTED

On both Nginx and OpenLiteSpeed you will need to connect to your server. See the following guides to get started:1

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Block on Nginx Option 1: HTTP/1.1 Method

Simply blocking HTTP/1.1 on a specific page is super easy.  Implementing multiple if statements on Nginx to only block if both conditions “A” and “B” (i.e. traffic is HTTP/1.1 and user-agent is not in the whitelist) are true is a little more complex. I modified the following gist for the rule detailed below:

https://gist.github.com/jrom/1760790

On Nginx we can make use of the *-main-context.conf include.

### 1. Create a Custom Nginx Config

On Nginx you can create a server-wide config that will apply to all sites or a site-specific config.

To create a server-wide config, run the following command:

```
/etc/nginx/extra.d/blockspam-main-context.conf
```

To create a site-specific config, run this command (replace site.url with your site’s domain name):

```
nano /var/www/site.url/nginx/blockspam-main-context.conf
```

### 2. Add Your Block Spam Configuration

Paste the following, and edit as necessary to target the correct URI for your website:

```
if ($request_uri ~* /contact/) {set $test A; }if ($server_protocol ~* "(HTTP/1.0|HTTP/1.1|HTTP/1.2)") { set $test "${test}B"; }if ( $http_user_agent !~* "(Googlebot|Bingbot|DuckDuckBot|facebot|cloudflare|Slurp|Alexa)" ) { set $test "${test}C"; }if ($test = ABC) { return 403;}
```

Or, if using a server-wide rule, you can target multiple pages like this:

```
if ($request_uri ~* "(/contact/|/contact-us|/get-in-touch/)") {set $test A; }if ($server_protocol ~* "(HTTP/1.0|HTTP/1.1|HTTP/1.2)") { set $test "${test}B"; }if ( $http_user_agent !~* "(Googlebot|Bingbot|DuckDuckBot|Facebot|cloudflare)" ) { set $test "${test}C"; }if ($test = ABC) { return 403;}
```

Save the file with CTRL+O followed by Enter, and then CTRL+X to exit nano.

This states that if:

### 3. Check and Reload Nginx

Check the Nginx configuration file with:

```
nginx -t
```

If no errors are returned, reload Nginx with:

```
gp ngx reload
```

Nginx will now block Eric Jones spam, all other types of junk on your contact pages.

 

## Block on Nginx Option 2: Referer Method

For this method we can make use of the *-wp-admin-ajax-context.conf Nginx include.

### 1. Create a Custom Nginx Config

This needs to be created on a site by site basis as you’ll be whitelisting your website’s specific URL.

Create your config with this command (replace site.url with your site’s domain name):

```
nano /var/www/site.url/nginx/blockspam-wp-admin-ajax-context.conf
```

### 2. Add Your Block Spam Configuration

Paste the following, and replace “site.url” with the URL for your website:

```
if ($http_referer !~* ^https://site.url/) {return 403;}
```

Save the file with CTRL+O followed by Enter, and then CTRL+X to exit nano.

### 3. Check and Reload Nginx

Check the Nginx configuration file with:

```
nginx -t
```

If no errors are returned, reload Nginx with:

```
gp ngx reload
```

Nginx will now block Eric Jones spam, all other types of junk on your contact pages.

 

## Block on OpenLiteSpeed

Section coming soon!

UPDATE: OpenLiteSpeed appears to handle RewriteCond %{SERVER_PROTOCOL} differently to Apache. We’re reaching out to the OLS team directly for clarification.

 

## Always Check Your Work

Once your block spam rules are in place, it’s a good idea to head over to Google Search Console and confirm that Google has no issue accessing your page/s.

The same goes for other accounts if you have them, or you can spoof them with a Chrome extension like User-Agent Switcher for Chrome.

 

## Other Alternative Solutions

I’ve personally used 2 other solutions that have provided good protection from Eric Jones and other spammers – these are numbers 1 and 3 below.

I’ve also used many that worked for a time, but then became worthless. Honey pots were a clever fix for a short while but are now mostly useless. Most plugins are largely the same in my experience. Three that work generally well are detailed below, plus a fourth option that should provide good protection as well.

### 1. Google ReCAPTCHA V3

Most contact forms integrate with Google reCAPTCHA V3 and it has done an excellent job of cutting down on spam on the few sites that I’ve used. It uses JavaScript to detect legitimate website visitors and it generally doesn’t interfere with UX like the earlier versions. Others also largely report good results, and it’s free to use.

### 2. hCaptcha

hCaptcha is a good alternative to Google’s reCAPTCHA for privacy reasons. There’s no invisible version like with reCAPTCHA V3 in the free version, but the challenges will help reduce spam.

### 3. Bot Test Question

Not all contact forms offer this functionality, but this has always done a great job of blocking spam in my experience. Right before the submit button, place a simple question that requires a correct answer for the form submission to be allowed.

For example: “What is 8+5?“. Automated tools can’t answer these questions and therefore cannot successfully submit emails.

### 4. Cloudflare Challenge on Contact Pages

If you wanted a simple solution that’s easy to implement (but may result in 5 second challenges to website visitors), then adding a Cloudflare firewall rule that just challenges all traffic to specific pages is another potential option too. It’s an intrusive security measure though.

### What About a Plugin like Cleantalk?

I’m hesitant to recommend the Cleantalk plugin as a solution. We’ve seen many cases where it’s caused database table locking which can lead to a whole server experiencing 502/504 errors. Those who use it do report good results, but we’ve seen too many support tickets where Cleantalk has been the direct cause of severe 502 errors.

I’m not aware of any other plugins that A LOT of people both use and recommend, however, Akismet does reportedly work well for members of the community and it doesn’t have any known caveats.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

