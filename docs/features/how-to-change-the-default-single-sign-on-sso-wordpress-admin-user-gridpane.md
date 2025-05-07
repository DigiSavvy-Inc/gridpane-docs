# How to Change the Default Single Sign On (SSO) WordPress Admin User | GridPane

# How to Change the Default Single Sign On (SSO) WordPress Admin User

 

2 min read 

### Table of Contents

 

## Introduction

GridPane’s Single Sign On (SSO) is a handy way to quickly log into your WordPress websites without needing to manually do so with your username and password. Full details can be found in this knowledge base article:

Using GridPane WP-Admin Single Sign On (SSO)

### How GridPAne SSO Works

By default, our SSO feature uses the WordPress user with the lowest ID number inside the wp_users database table. It starts with WordPress user #1, and if that doesn’t exist, tries #2, and so on.

If you would like to change this to another user, it’s a quick simple process.

 

## Step 1. Check Your User ID

To locate your desired user ID number, open up PHPMyAdmin for your website by clicking on the database icon next to your website on the Sites page:

This will automatically log you in. From here, select the database and click through to wp_users. User ID numbers are displayed in the ID column, followed by the user_login column.

Note your user’s ID number and proceed to the step below.

 

## Step 2. Update Your SSO ID

To get started you’ll need to connect to your server. If this is your first time doing so please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

The WordPress user ID the SSO feature checks first is contained in the wpadmin_id.env in your websites /logs directory.

By default, it contains “1“. You can update this with the ID number of the WordPress user you want SSO to log in to your website as.

### 1. Update the wpadmin_id.env file

Edit the file with the following command, replacing “site.url” with your website’s URL:

```
nano /var/www/site.url/logs/wpadmin_id.env
```

Switch out the number, then save the file with CTRL+O followed by Enter. Exit the file with CTRL+X.

### 2. Confirm Your Work

Back inside your GridPane account, click on the SSO button, and confirm you’re now logged in as the correct admin user.

Once done, you’re all set!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

