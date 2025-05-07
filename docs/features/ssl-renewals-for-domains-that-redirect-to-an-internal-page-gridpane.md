# SSL Renewals for Domains that Redirect to an Internal Page | GridPane

# SSL Renewals for Domains that Redirect to an Internal Page

 

6 min read 

## Intro

If you have a website where you’ve set up a redirect that looks like this via an Nginx configuration file:

old-domain.com —-> new-domain.com/something

This article is for you.

Regular redirect domains that are added via the Site customizer will not experience the same SSL renewal errors.

## The Renewal Error

If you’ve received an SSL renewal error, the first thing you need to do is head to the SSL log for that website. This will give a clear reason for why Let’s Encrypt has been unable to renew the SSL.

In this case, it will look similar to this:

 

```
1 renew failure(s), 0 parse failure(s)
IMPORTANT NOTES:
- The following errors were reported by the server:

Domain: old-website.com
Type: unauthorized
Detail: Invalid response from
https://new-website.com/something//.well-known/acme-challenge/199nbYyxhysPwgs8_bXLPsdf9WERfsdfETz0B1F68r
[199.199.199.199]: "\r\n404 Not
Found\r\n\r\n# 404 Not
Found

\r\nnginx\r\n"

Domain: www.old-website.com
Type: unauthorized
Detail: Invalid response from
https://new-domain.com/something//.well-known/acme-challenge/WYg8VQnFCPHSY9liTvew8fWslA_ErsvqElEWoK3xM
[199.199.199.199]: "\r\n404 Not
Found\r\n\r\n# 404 Not
Found

\r\nnginx\r\n"

To fix these errors, please make sure that your domain name was
entered correctly and the DNS A/AAAA record(s) for that domain
contain(s) the right IP address.
```

Here we can see that the redirect is confusing Let’s Encrypt, taking them to a different URL.

 

## How to Fix it

You have two options to fix this. We recommend the first if possible as it’s the easiest method and will prevent this from happening again in the future.

### Option 1: Switch to a DNS API Integration

Use a DNS Integration and provision an SSL via either the regular DNS API method or the Challenge method. This method doesn’t rely on Let’s Encrypt checking your live site, and so the redirect won’t affect the renewal.

The following articles detail provisioning an SSL certificate via the DNS API methods:

### Option 2: Reconfigure your redirect

We now have a configuration available that will allow you to solve this issue once and for all. Continue below.

 

## Let’s Encrypt and the .well-known Directory

One of the challenges that comes with this kind of redirect is that once it’s in place, by default, when Let’s Encrypt requests access to the .well-known directory the request is redirected away and it cannot confirm domain ownership. Without this, your website is not considered eligible for either a new SSL or an SSL renewal if you’re using the webroot method.

To ensure that your Alias domain’s SSL can provision/renew if you’re not using our DNS API integrations, we need to ensure that Let’s Encrypt can still access the .well-known directory once the redirect is in place.

UPDATE: As of May 3rd 2021, we have adjust our configs to allow for this.

We now include the following for Primary domains:

```
location ~ /\.well-known {allow all;include /var/www/${primary_site}/nginx/*well-known-${primary_domain}-context.conf;include /var/www/${primary_site}/nginx/*well-known-context.conf;}include /var/www/${primary_site}/nginx/*-main-${primary_site}-context.conf;
```

And this for Alias domains:

```
location ~ /\.well-known {allow all;include /var/www/${primary_site}/nginx/*well-known-${add_on_domain}-context.conf;include /var/www/${primary_site}/nginx/*well-known-context.conf;}include /var/www/${primary_site}/nginx/*-main-${add_on_domain}-context.conf;
```

This means that we can allow requests to the .well-known directory to take place before the includes where we add our redirect.

 

## Fixing Primary Domain Redirects

The following assumes you have followed our guide on how to setup redirects in the past (now updated to include the new .well-known info):

Nginx Redirects Examples

### Step 1. Connect to your server

SSH into your server.

### Step 2. Remove Your Previous Redirect Config

To remove your configuration file, locate and use the rm command followed by the /path/to/file/redirect.conf. For example:

```
rm /var/www/site.url/new-domain-redirect-root-context.conf
```

### Step 3. Create the .well-known config

We need to create 2 configs to set this redirect up and have it work with Let’s Encrypt. The first is the .well-known config as follows: /var/www/{primary.domain}/nginx/well-known-main-context.conf

Create the file with the following command, switching out site.url with your domain name:

```
nano /var/www/site.url/nginx/well-known-main-context.conf
```

Add the following to file:

```
location ~ /\.well-known {
allow all;
}
```

Next press CTRL+O to save the file, followed by Enter. Close nano with CTRL+X.

### Step 4. Create the Redirect Config

Run the following command to create the redirect configuration file, switching out site.url for your domain:

```
nano /var/www/site.url/nginx/redirect-root-context.conf
```

Add your redirect in the following format, switching out new-domain.url for the domain of the website you want to redirect to:

```
return 301 https://new-domain.url$request_uri;
```

### Step 5. Check and Restart Nginx

Make sure that the Nginx conf files are ok and then reload Nginx. Check the syntax with:

```
nginx -t
```

If no errors are present, reload with:

```
gp ngx reload
```

### STEP 6. RENEW YOUR SSL

Run this command to renew your SSL certificate:

```
certbot-auto renew
```

Now that the redirect is no longer preventing Let’s Encrypt from accessing the .well-known directory, the SSL renewal will go through.

### Done!

You’re all set! Check your redirect is all good and have a great day!

 

## Fixing Alias Domain Redirects

The following assumes you have followed our guide on how to setup redirects in the past (now updated to include the new .well-known info):

Nginx Redirects Examples

### Step 1. Connect to your server

SSH into your server.

### Step 2. Edit Your Redirect Config

Navigate to your websites Nginx directory with the following command (swapping out site.url for your domain name):

```
cd /var/www/site.url/nginx
```

Next run:

```
ls -l
```

This will list the files in the directory, and you’re looking for a file named like so (with alias.url being the name of your alias domain): redirect-main-alias.url-context.conf

It may not start with “redirect” if you have given it a different name.

Edit the file with nano, switch out the name and alias-url parts as applicable):

```
nano name-main-alias.url-context.conf
```

Now you need to edit the file to contain the following (switching out newdomain.com/en for your own redirect):

```
location ~ /\.well-known {
   accept all;
}

location ~ / {
return 301 https://newdomain.com/en$request_uri;
}
```

CTRL+O followed by Enter to save the file, CTRL+X to exit nano.

### Step 3. Check and Restart Nginx

Make sure that the Nginx conf files are ok and then reload Nginx. Check the syntax with:

```
nginx -t
```

If no errors are present, reload with:

```
gp ngx reload
```

### STEP 4. RENEW YOUR SSL

Run this command to renew your SSL certificate:

```
certbot-auto renew
```

Now that the redirect is no longer preventing Let’s Encrypt from accessing the .well-known directory, the SSL renewal will go through.

### Done!

You’re all set! Check your redirect is all good and have a great day!

 

 

### Note

Please note this will require an updated config, any alias domains configs updated since May 3rd 2021 will have these includes, however any older config that hasn't been regenerated recently will not. We do not automatically replace in-place configs. The domain action such as changing www/root routing, or site actions such as changing cache types will regenerate any pre-existing config files to the latest version.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

