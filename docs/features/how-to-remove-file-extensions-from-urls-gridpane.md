# How to remove file extensions from URLs | GridPane

# How to remove file extensions from URLs

 

2 min read 

We recently had an inquiry asking how to remove the file extensions from URLs when linking directly to them.

In this particular case, it was how to remove the “.txt” from a URL so that:

gridpane.com/folder/somefile.txt

Becomes:

gridpane.com/folder/somefile

This article will walk you through how to exclude the file extension from any file of your choice.

## Nginx try_files and rewrites

We need to add a try_files directive to your website’s nginx.conf, and to do this we need to create a custom *-main-context.conf inside your website’s Nginx directory.

The * part of this file name can be anything you choose, for example: fileext-main-context.conf.

Any code place here will act as if this code is inside of the server {} block in the nginx.conf file for your website. There is no need to include server {}.

Let’s get started.

## Step 1. SSH into your Server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Create your config

We’ll be creating a file called “fileext-main-context.conf”. Run the following command switching out “site.url” for your website’s domain:

```
nano /var/www/site.url/nginx/fileext-main-context.conf
```

## Step 3. Edit and add your code for the specific file extension you wish to remove

The following is a block of code that will remove the “.txt” extension from text files like in the example at the beginning of this article.

If you’re removing a different extension you can simply switch out “txt” in the example code below for your file extension (e.g. for .pdf files, replace txt with pdf).

The code below also assumes that your files will be located somewhere inside /wp-content. If they’re located elsewhere be sure to alter the first line accordingly.

```
location /wp-content { 
 try_files $uri $uri/ @rm-ext;
 }

location ~ .txt$ {
 try_files $uri =404;
 }

location @rm-ext {
 rewrite ^(.*)$ $1.txt last;
 }
```

Hit Ctrl+O and then press enter to save the file. Then Ctrl+X to exit nano.

## Step 4. Check and reload Nginx

We now need to test our Nginx syntax with:

```
nginx -t
```

If there are no errors present, reload Nginx with the following command:

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

