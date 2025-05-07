# IFrames, X-Frame-Options and how to disable Clickjacking protection | GridPane

# IFrames, X-Frame-Options and how to disable Clickjacking protection

 

3 min read 

### Table of Contents

 

## What is Clickjacking?

Clickjacking (classified as a User Interface redress attack, UI redress attack, UI redressing) is a malicious technique of tricking a user into clicking on something different from what the user perceives, thus potentially revealing confidential information or allowing others to take control of their computer while clicking on seemingly innocuous objects, including web pages.– Wikipedia

 

## GridPane Clickjacking Protection

By default, GridPane enables clickjacking protection on all websites. This is an important security measure designed to keep your website and your visitors safe.

### IFrames

An IFrame is a way of inserting content from an external source into your website. Iframes by their very nature are insecure and by enabling them you’re opening up potential security vulnerability which could direct unknowing website visitors to unsafe sites.

Clickjacking protection will block iframes from external sources until you manually disable it.

There are, however, some cases which require clickjacking to be disabled in order to work, and we have a GP-CLI command that you can run to disable it on specific websites.

### X-Frame-Options

The X-Frame-Options response header lets a browser know whether it’s allowed to render a page inside an <iframe>, <frame>, <embed> or <object> tag.

Learn more about the X-Frame-Options response header here:https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options

 

## Disabling Clickjacking

If you need to disable clickjacking we recommend configuring and enabling CSP headers in its place. This will allow you to set sources for your iframes at a granular level. You can learn more about CSP headers in the following places:

How to create a Content Security Policy (CSP Header)

https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP

### Option 1. Disable Clickjacking in the Customizer

You can disable Clickjacking on any of your websites directly inside your account on the Sites page. Simply click on the name of the website to open up the customizer, and you will see the Clickjacking toggle in the Settings tab:

### Option 2. Disable Clickjacking via GP-CLI

To turn off clickjacking protection on a specific website via GP-CLI, SSH into your server and run the following command (replacing “site.url” with your websites domain name):

```
gp site site.url -clickjacking-protection-off
```

Example:

```
gp site mywebsite.com -clickjacking-protection-off
```

If you need to re-enable it you can always do so in your website customizer, or run the following:

```
gp site site.url -clickjacking-protection-on
```

 

## Disabling Clickjacking for HTML and Other Static Files

In the case of HTML or other static files, in order to remove the X-Frame-Options you will need to manually add an Nginx include in the static context.

### Step 1. Create the config

To do this, first connect to your server over SSH, and then run the following command (replacing site.url for your websites URL):

```
nano /www/site.url/nginx/click-jack-static-context.conf
```

Add the following statement in the file:

```
more_clear_headers "x-frame-*";
```

Now save the file with CTRL+O and then Enter. Next hit CTRL+X to exit nano.

### Step 2. Check and reload Nginx

You will then need to check and reload Nginx.

Test your nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

