# An Introduction to Cross-Origin Resource Sharing (CORS) | GridPane

# An Introduction to Cross-Origin Resource Sharing (CORS)

 

10 min read 

### Table of Contents

 

## Introduction

Cross Origin Resource Sharing (CORS) policies are HTTP response headers that are used to increase the security of a website. A request for a resource (for example a font file, JS, CSS, etc) made by a source outside of your domain name (the origin) is known as a cross-origin request. You can create a CORS policy to allow and manage cross-origin requests.

At first glance CORS may seem similar to a Content Security Policy (CSP), however, their functions are very different.

A CSP determines exactly what is allowed to run on your own website – for example, you can specify where fonts are allowed to be loaded from on your site.

A CORS policy allows you to share assets on your website with another domain. You can specify exactly who is allowed to access them, and also exactly how they are allowed to access them. An example of a use case for this would be connecting your website to a CDN. CORS is particularly useful for today’s modern web as sharing resources such as fonts, icons, JS, etc is becoming more and more common.

 

## Same-Origin Policy

Before we dive into creating a CORS policy, it’s important to understand the same-origin policy.

By default, the same-origin policy will be enforced on your website. This policy states that absolutely no cross-origin resource sharing can take place. However, you can create a CORS policy that essentially overrides this.

For two URLs to have the same origin, they must share: –

The port number only applies if specified and I include it to be thorough, but it’s not necessary for our purposes. In this article, we’ll focus on the domain and HTTP protocol.

CORS policies give you the option to change the default same-origin policy to something less strict and allow for certain types of cross-origin requests.

 

The same-origin policy is a critical security mechanism that restricts how a document or script loaded from one origin can interact with a resource from another origin. It helps isolate potentially malicious documents, reducing possible attack vectors.

[Source: Mozilla](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)

The same-origin policy is important for the web to remain a safe place and this is the reason that it’s enforced by default.

 

## How does CORS work?

A CORS policy allows you to create exceptions to the single-origin policy. Just like a CSP, it allows you to be very specific in what you allow to be shared, and how you share it.

In a nutshell, when you load a website it instructs your browser where to download resources in order to build that webpage. If it specifies resources from another origin (a different HTTP protocol and/or domain name), a CORS policy allows your browser and the server hosting those resources to communicate and determine whether or not a cross-origin request is safe. This decision is determined by CORS HTTP request and HTTP response headers (or the same-origin policy if no CORS policy is in place).

The most common request is the GET request. If the Access-Control-Allow-Origin header is set up to allow certain types of assets to be available to all (*) domains, this request method is usually allowed by most servers.

Other HTTP requests methods such as PATCH PUT DELETE, however, are normally denied by default to prevent malicious behavior. This prevents outside servers from being able to edit or delete your server’s assets.

Other modifying types of requests can be sent with the OPTIONS header. These are known as preflight requests and are sent before the actual request to determine whether it’s safe. The server will accept or reject the request based on the policy that’s in place.

 

## CORS HTTP Headers

The following are the available CORS HTTP headers and Mozilla has a quick breakdown of what each HTTP header does here: CORS Headers.

### CORS HTTP Request Headers

### CORS HTTP Response Headers

The Access-Control-Allow-Origin is the most important header we need to understand. The same-origin policy tells a browser to deny cross-origin requests. The Access-Allow-Origin-Header lets you instead allow and specify exactly which external domains are allowed access to your server assets.

If you know that an external domain is safe (for example another website that you own), then you can provide access to that domain and no one else. Properly configuring this header is a necessity to keep your server assets secure.

 

### Pre-Flight Requests

As mentioned above, most servers will allow GET requests, but other types include:

Browsers will create a preflight request for more complex HTTP requests. The preflight request is used to ask the server whether the appropriate permissions are in place before the actual request itself is made. This gives the server a chance to tell the browser whether it should proceed and send the request, or instead return an error to the client.

 

## A Simple CORS Policy Example

 

## A CORS Policy Example with Preflight Requests

A browser makes the following preflight request:

```
Origin: https://example.comAccess-Control-Request-Method: DELETEAccess-Control-Request-Headers: A-Custom-Header
```

For example purposes, the server is configured to allow these requests and responds with:

```
Access-Control-Allow-Origin: https://example.comAccess-Control-Allow-Methods: GET, POST, DELETEAccess-Control-Allow-Headers: A-Custom-Header
```

This response says that GET POST DELETE are permitted request methods and A-Request-Header is a permitted request header.

As the requested headers are permitted the browser will then process the cross-origin request.

 

## Building a Simple CORS Policy on Nginx

On GridPane Nginx you have the option of either creating a CORS Policy on a website-by-website basis, or you can create one for all of the sites on your server.

An example of when all sites on a server may make sense would be if all your websites were being loaded by the same CDN. If the CORS policy you’re creating doesn’t apply to all websites then you should only implement it on a per website basis.

 

### Step 1. Defining the rules

First, you need to decide exactly what files you’re going to allow access to. For the few applicable WordPress use cases, simply clearing the existing header and adding the  following is the simplest solution:

```
more_clear_headers "Access-Control-Allow-Origin";more_set_headers "Access-Control-Allow-Origin: *";
```

However, you can specify the file types you want to modify your access control policy as follows:

```
location ~* \.(eot|ttf|woff|woff2|font.css|css|js|gif|png|jpe?g|svg|ico|webp)$ {more_clear_headers "Access-Control-Allow-Origin";more_set_headers "Access-Control-Allow-Origin: https://domain.com";}
```

The above allows all of those filetypes to be accessible to any external domain.

You can further narrow down to specific resources like as follows:

```
location ~* \.(eot|ttf|woff|woff2)$ {more_clear_headers "Access-Control-Allow-Origin";more_set_headers "Access-Control-Allow-Origin: https://domain.com";}
```

The above narrows files types down to only allow font files to be accessible by https://specifidomain.com. No other domains can access those files, and this domain cannot access any other filetypes on your server.

 

### Step 2. Connect to your server

To get started, please see the following guides if you haven’t connected to one of your servers before:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

If you’re setting up a CORS policy for a specific site, follow the steps in 3.1. If you’re setting up a policy for all the websites on a server, skip 3.1 and follow the steps in 3.2 a little further down.

 

### 3.1 Site Specific CORS Policy

Once connected, navigated to your website’s Nginx folder with the following command (replacing “site.url” with your domain):

```
cd /var/www/site.url/nginx
```

Create a file named cors-main-context.conf with the following:

```
nano cors-main-context.conf
```

Add your code block to the file, and then save it with CTRL+O and then Enter. You can now exit nano with CTRL+X. Now proceed to step 4.

### 3.2 CORS Policy for ALL websites

First, create your CORS config with:```
nano /etc/nginx/extra.d/cors-main-context.conf
```

Add your code block to the file, and then save it with CTRL+O and then Enter. You can now exit nano with CTRL+X.

 

### Step 4. Check your Nginx Syntax and Reload Nginx

We now need to test our nginx syntax with:

```
nginx -t
```

If there are no errors present, reload nginx with the following command:

```
gp ngx reload
```

Your header is now in place.

 

### Step 5. Clear ALL Website Caches

To ensure your header is served, clear all your website caches and any CDN level caches (including Cloudflare if applicable).

You can now check your site.

 

## Further Reading

If you’d like further reading on CORS, I highly recommend you check out Mozilla’s article on the topic:

Mozilla: Cross-Origin Resource Sharing (CORS)

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

