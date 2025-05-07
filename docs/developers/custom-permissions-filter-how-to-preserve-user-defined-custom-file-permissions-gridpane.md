# Custom Permissions Filter: How to Preserve User-Defined Custom File Permissions | GridPane

# Custom Permissions Filter: How to Preserve User-Defined Custom File Permissions

 

1 min read 

GridPane has a worker function that will automatically reset your WordPress website file permissions. However, there may be instances where you need a specific file’s permissions to be set differently, and for this you can use our custom permissions filter to exclude them from being overwritten.

## Using the Custom Permissions Filter

### Step 1. Connect to your Server

To get started, first connect to your server. If this is your first time connecting to a GridPane server, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Set Your Custom Owner/Permissions

Set your permissions with:

```
chmod permissions your-file-name
```

To learn more about managing permissions, this article offers a great, in-depth rundown with examples:

https://www.redhat.com/sysadmin/manage-permissions

 

### Step 3. Create the custom.perms file

The custom permissions filter uses a file called custom.perms. This needs to be added to the website’s main directory: /var/www/site.url. Create the file with the following command (replacing site.url for your website’s URL):

```
nano /var/www/site.url/custom.perms
```

Inside that file add the absolute file path to any directories or files that have custom perms that you want to maintain, these file paths should be delimited with a colon : at either end, one per line. For example:

```
:/var/www/site.url/htdocs/wp-content/themes/whatever/style.css:
```

The worker that ensures that all site directories and files have WordPress perms will ignore any file path included in that file.

Save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

And that’s it! You’re all set.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

