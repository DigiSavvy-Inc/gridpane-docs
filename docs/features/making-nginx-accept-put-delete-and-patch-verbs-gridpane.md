# Making Nginx Accept PUT, DELETE and PATCH verbs | GridPane

# Making Nginx Accept PUT, DELETE and PATCH verbs

 

4 min read 

 

### UPDATE - PUT and DELETE Requests

PUT and DELETE requests are no longer blocked on Nginx servers by default, however, you may still need to configure the dav_methods outlined in this article for your website if the requires them.

## Introduction

Modern servers do not allow for PUT DELETE PATCH requests to be available by default.

On Nginx, these aren’t even possible actions within the core HTTP module. To allow PUT and DELETE requests on Nginx, you need to compile in an extra module and make changes for each site. PATCH requires even more additional steps, and it’s considered to be a dangerous HTTP verb to have open. If a plugin or service you’re using requires PATCH to be open, you may want to talk directly with their development team and to discuss security concerns.

The lead developers of WordPress are aware that most servers don’t allow these methods, and so they have built  an override method into the REST API to take this into account.

The REST API allows all CRUD (Create, Read, Update, and Delete) operations available via PUT DELETE PATCH to be carried out by either passing the method in the request as a query parameter or using a specific header containing the method:

Using the ?_method={HTTP_VEBR} query parameter method override:

```
http
POST /wp-json/wp/v2/posts/42?_method=DELETE
```

Using the X-HTTP-Method-Override header method override:

```
http
POST /wp-json/wp/v2/posts/42
Host: example.com
X-HTTP-Method-Override: DELETE
```

This way, ALL insecure WP-API CRUD actions can be achieved using POST requests, and your servers can be securely locked down to POST GET HEAD PURGE methods.

On GridPane, making use of the REST API also allows for our 6G/7G firewalls to be enabled with no conflicts, allowing for even further security.

### Themes/Plugins We Know Of

Below are the following plugins that we’re aware of that require these settings:

You can make your Nginx server accept these verbs in just a few steps – follow along below.

 

 

### Special Note For 6G and 7G WAF Users

If you use the 6G or 7G WAF you'll also need to create an exclusion for "bad-methods". The easiest way to do this is inside the security tab, or you can run the following command (switching out site.url for your domain name):
gp site site.url 6g -bad-methods offgp site site.url 7g -bad-methods offFull documentation can be found here: -
1. 6G WAF
2. 7G WAF

## Step 1. SSH into your server

Please see the following article to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Create a root level conf file for these verbs

The easiest way to do this is by using nano and adding the file directly on the server like this (make sure to replace example.com with your own domain):

```
nano /var/www/example.com/nginx/http-verbs-root-context.conf
```

Now inside the nano editor, add into the file this line using:

```
dav_methods PUT DELETE;
```

Once complete, CTRL + O, and then Enter save the file, and then exit nano with CTRL+X.

 

## Step 3. Add the verbs to the “more_set_headers” directive

Next, nano to the config file with the following command:

```
nano /etc/nginx/extra.d/headers-http-context.conf
```

Add PUT DELETE PATCH to the more_set_headers allow directive and into the if guard block. The config file should look like this:

```
more_set_headers "allow: GET, POST, HEAD, PURGE, PUT, DELETE, PATCH" always;

if ($request_method !~ ^(GET|POST|HEAD|PURGE|PUT|DELETE|PATCH)$) {
  return 405;
}
```

Once complete, CTRL + O, and then Enter save the file, and then exit nano with CTRL+X.

 

## Step 4. Ensure our changes persist

Next, create the _custom directory and place a copy of the file you just edited in there:

```
mkdir /etc/nginx/extra.d/_custom
```

Followed by:

```
cp /etc/nginx/extra.d/headers-http-context.conf /etc/nginx/extra.d/_custom/headers-http-context.conf
```

This will ensure that our changes persist, and aren’t overwritten at a later date.

 

## Step 5. Check and reload Nginx

Check the Nginx syntax with:

```
nginx -t
```

If there are no errors, then run:

```
gp ngx reload
```

You’re all set! Now you just need to check your work and ensure that your plugin is working correctly.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

