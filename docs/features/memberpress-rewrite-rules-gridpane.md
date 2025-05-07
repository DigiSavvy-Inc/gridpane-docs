# MemberPress Rewrite Rules | GridPane

# MemberPress Rewrite Rules

 

2 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

Before we begin, this article is based on implementing the rewrite rules as outlined directly by MemberPress in their documentation:

https://docs.memberpress.com/article/179-understanding-rewrite-rules

In this article they state: “MemberPress does not officially support Nginx as a web-server.“

Should any issues arise, these would require the attention of the MemberPress team and it’s not something that our support team will be able to help you troubleshoot.

That all out the way, let’s get started!

## Step 1. SSH into your server

To implement these rules you will need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Create memberpress-main-context.conf

To implement these rewrite rules on your website, we need to to add the configs to a file in your `/site.url/nginx` directory using the `*-main-context.conf` include wildcard.

To keep things organised, we’ll name the file `memberpress-main-context.conf`.
### Create the file

You can create this file with the following command (switching out “site.url” for your websites domain):
```
nano /var/www/site.url/nginx/memberpress-main-context.conf
```

For example:
```
nano /var/www/gridpane.com/nginx/memberpress-main-context.conf
```

This will both create the file and open it with the nano editor ready for the next step.

### Paste your config

Paste the following code into the file (again switching out “site.url” for your domain):
```
location ~* \.(zip|gz|tar|rar|doc|docx|xls|xlsx|xlsm|pdf|mp4|m4v|mp3|ts|key|m3u8)$ {
                # Setup lock variables
                set $mplk_uri "/wp-content/plugins/memberpress/lock.php";
                set $mplk_file "/var/www/site.url/htdocs/wp-content/uploads/mepr/rules/${cookie_mplk}";

                # don't lock the lock uri
                if ($uri ~* "^/(wp-admin|wp-includes|wp-content/plugins|wp-content/themes)") { break; }

                # redirect if the lock file's a dir or doesn't exist
                if (-d $mplk_file) { rewrite ^ $mplk_uri last; }
                if (!-e $mplk_file) { rewrite ^ $mplk_uri last; }
        }
```

You can now hit Ctrl+O and then press Enter to save the file. Then Ctrl+X to exit nano.
## Step 3. Check and reload Nginx

We now need to test our Nginx syntax with:
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

