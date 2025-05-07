# Self Help Tools: Reset Application File Permissions | GridPane

# Self Help Tools: Reset Application File Permissions

 

1 min read 

## Introduction

If any of your website installations files are, for some reason, NOT owned by your website’s system user, your website will not be able to access the files.

This can happen if you edit any of your website files as the root user, and it can result in 500 errors, 403 errors, fatal errors, etc.

Fortunately, this is easy and quick to fix directly inside of your GridPane account dashboard.

 

## Reset Permissions via Self Help Tools

First visit the Tools section by clicking the link in the main menu.

Here you will see the quick fix panel at the top of the main window:

GridPane will check all directory and file permissions to make sure they’re all correct. This tool is particularly useful when there are errors or other strange behaviors coming from your site. Check the Event Output Viewer for confirmation the process has been completed.

 

## Alternative Option: Reset Permissions via GP-CLI

While resetting permissions is easily done inside of your account dashboard, you can also easily do this via GP-CLI directly on your server.

If you’d like to try this out but have never connected to one of your servers before, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

When connected to your server, you can run the following command to fix permissions for your website (replace site.url with your website URL):

```
gp fix perms site.url
```

For example:

```
gp fix perms yourwebsite.com
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

