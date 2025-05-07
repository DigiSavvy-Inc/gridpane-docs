# Exclude a Custom WP Ultimo Sign-Up URL from the Cache | GridPane

# Exclude a Custom WP Ultimo Sign-Up URL from the Cache

 

2 min read 

If you’re using a custom sign up URL for your WP Ultimo website and it doesn’t end in “.php”, then you may need to exclude that page from your websites cache. If you’re using our server caching options, below is a walk through on how to do this, and below is an example of what happens if the sign up page is cached:

## Step 1: Log into your server as root

Use your favorite SSH client and connect to your server IP as root. If you’re not sure how to do this, please see the following articles to get started:

Generate your SSH Key:

Generate SSH Key on Mac

Generate SSH Key on Windows with Putty

Generate SSH Key on Windows with Windows Subsystem for Linux

Generate SSH Key on Windows with Windows CMD/PowerShell

Add your SSH Key to GridPane:

Add default SSH Keys

Add/Remove an SSH Key to/from an Active GridPane Server

Connect to your server:

Connect to a GridPane server by SSH as Root user.

## Step 2: Add your cache exclusion

If you’re using Redis page caching, type:

```
nano /var/www/site.url/nginx/custom-skip-redis-cache-context.conf
```

The “site.url” is the real domain of your site.

If you’re using FastCGI page caching, type:

```
nano /var/www/site.url/nginx/custom-skip-fcgi-cache-context.conf
```

The “site.url” is the real domain of your site. For our example “waas.monster” from the

Then copy the below information and paste inside your SSH client. On most machines this will be a right click with your mouse, not a CTRL + V.

```
if ($request_uri ~* "(/signup*)") {
 set $skip_cache 1;
 set $skip_reason "${skip_reason}-request_uri";
}
```

The top line should contain your sign up url. For example, if your sign up url was superwaas.com/signup, the above would work correctly. If it was “superwaas.com/register” the top line would be:

```
if ($request_uri ~* "(/register*)") {
```

CTRL+O and then press Enter to save the file. You can then exit nano with CTRL+X.

## Step 3: Test your nginx (important)

You’ll want to run an “nginx -t” on the command line. This will test your configs, and if all is well, it will show the below message. If it shows any failures, or any message other than what is below, do NOT proceed to step 4:

```
root@servername:~# nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
root@servername:~#
```

## Step 4: Reload nginx configuration

Remember, if you didn’t have a successful test above, do not proceed. Finally, reload your nginx config by running “gp ngx reload” on the command line.

You’re now all set 🙂

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

